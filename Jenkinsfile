pipeline {
    agent none
    environment {
        DOCKER_REGISTRY = '374981481454.dkr.ecr.us-east-1.amazonaws.com'
    }
    stages {
        stage('Build') {
            environment{
                VERSION = sh (script: "git rev-parse --short HEAD", returnStdout: true)
            }
            agent {
                label 'ec2_agent'
            }
            steps {
                sh 'docker compose build'
                sh '''
                    docker tag  \
                        ${DOCKER_REGISTRY}/prueba_nginx:latest  \
                        ${DOCKER_REGISTRY}/prueba_nginx:${VERSION} 
                   '''
            }
        }
        stage('Push'){
            environment{
                VERSION = sh (script: "git rev-parse --short HEAD", returnStdout: true)
            }
            agent{
                label 'ec2_agent'
            }
            steps{
                sh '$(aws ecr get-login --no-include-email --region us-east-1)'
                sh 'docker compose push'
                sh 'docker push ${DOCKER_REGISTRY}/prueba_nginx:${VERSION}'
            }
        }
        stage('Deploy'){
           agent{
               label 'ec2_agent'
           }
           steps{
                sh 'docker compose up -d'
            }
        }
        // stage('Clean') {
        //     agent {
        //         label 'ec2_agent'
        //     }
        //     steps {
        //         sh 'docker system prune -f'
        //     }
        // }
    }
}

