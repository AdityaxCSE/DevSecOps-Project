pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
	    IMAGE_TAG = "${env.BUILD_NUMBER}"
	    N8N_WEBHOOK_URL = "http://65.0.126.229:5678/webhook/cve-analysis"
    }

    stages {
        stage('Build') {
            steps {
                echo "Triggered by GitHub webhook"
            }
        }
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/AdityaxCSE/DevSecOps-Project.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('File System Scan') {
            steps {
                sh 'trivy fs --format table -o trivy-fs-report.html .'
            }
        }
        
        stage('SonarQube SAST Scan') {
            steps {
                withSonarQubeEnv('sonarserver') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=BoardGame -Dsonar.projectKey=BoardGame \
                            -Dsonar.java.binaries=. '''
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        
        stage('Build Application') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('Publish Artifacts to Nexus') {
            steps {
                withMaven(globalMavenSettingsConfig: 'global-maven-settings', jdk: 'jdk17', maven: 'maven3', traceability: true) {
                    sh 'mvn deploy'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                    sh 'docker build -t adi35tya/boardgameapp:${IMAGE_TAG} .'
            }
        }
        stage('Docker Image Scanning') {
            steps {
                sh 'trivy image --format table -o trivy-image-report.html adi35tya/boardgameapp:${IMAGE_TAG}'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-cred', url: 'https://index.docker.io/v1/') {
                    sh 'docker push adi35tya/boardgameapp:${IMAGE_TAG}'
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://172.31.24.163:6443') {
                    sh '''
                      sed -i "s|__IMAGE_TAG__|${IMAGE_TAG}|g" deployment-service.yaml
                      kubectl apply -f deployment-service.yaml
                    '''
                }
            }
        }
        stage('verify the deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://172.31.24.163:6443') {
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }
        }
        stage('Extract CRITICAL CVEs') {
            steps {
                sh '''
                grep -i "CRITICAL" trivy-*-report.html \
                | grep -oE "CVE-[0-9]{4}-[0-9]+" \
                | sort -u \
                > critical-cves.txt || true

                echo "===== CRITICAL CVEs FOUND ====="
                if [ -s critical-cves.txt ]; then
                    cat critical-cves.txt
                else
                    echo "No CRITICAL CVEs found"
                fi
                '''
            }
        }

        stage('Send CVEs to n8n for AI Analysis') {
            steps {
                sh '''
                if [ -s critical-cves.txt ]; then
                    curl -X POST ${N8N_WEBHOOK_URL} \
                        -H "Content-Type: text/plain" \
                        --data-binary @critical-cves.txt
                else
                    echo "Skipping n8n call – no CRITICAL CVEs"
                fi
                '''
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: '''
                critical-cves.txt,
                trivy-fs-report.html,
                trivy-image-report.html
            ''', fingerprint: true
            script {
                def jobName = env.JOB_NAME
                def buildNumber = env.BUILD_NUMBER
                def pipelineStatus = currentBuild.result ?: 'UNKNOWN'
                def statusUpper = (pipelineStatus ?: 'UNKNOWN').toUpperCase()
                def bannerColor = pipelineStatus.toUpperCase() == 'SUCCESS' ? 'green' : 'red'
                
                def body = """
                            <html>
                            <body>
                            <div style="border: 4px solid ${bannerColor}; padding: 10px;">
                            <h2>${jobName} - Build ${buildNumber}</h2>
                            <div style="background-color: ${bannerColor}; padding: 10px;">
                            <h3 style="color: white;">
                            Pipeline Status: ${pipelineStatus.toUpperCase()}
                            </h3>
                            </div>
                            <p>Check the <a href="${env.BUILD_URL}">console output</a>.</p> 
                            </div>
                            </body>
                            </html>
                        """
                
                emailext(
                    subject: "${jobName} - Build ${buildNumber} - ${statusUpper}",
                    body: body,
                    to: 'gamerzwar37@gmail.com',
                    from: 'knpaditya2001@gmail.com',
                    replyTo: 'knpaditya2001@gmail.com',
                    mimeType: 'text/html',
                    attachmentsPattern: 'trivy-*-report.html'
                )
                    
                }
            }
        }
    }
