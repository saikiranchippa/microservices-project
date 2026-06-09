pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t saikiran2233/recommendationservice:latest ."
                    }
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                sh '''
                trivy image \
                --severity HIGH,CRITICAL \
                --exit-code 1 \
                saikiran2233/recommendationservice:latest
                '''
            }
        }

        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push saikiran2233/recommendationservice:latest "
                    }
                }
            }
        }
    }
}
