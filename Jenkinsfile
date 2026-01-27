pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
	    IMAGE_TAG = "${env.BUILD_NUMBER}"
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
    }
    
    post {
        always {
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
                    to: 'knpaditya2001@gmail.com',
                    from: 'jenkins@example.com',
                    replyTo: 'jenkins@example.com',
                    mimeType: 'text/html',
                    attachmentsPattern: 'trivy-*-report.html'
                )
                    
                }
            }
        }
    }
