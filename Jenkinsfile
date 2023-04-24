pipeline {
    agent none
    parameters {
        string(name: 'MESSAGE', defaultValue: 'Hello World!', description: 'Title')
    }
    environment {
        DOCKER_REGISTRY = '374981481454.dkr.ecr.us-east-1.amazonaws.com'
    }
    stages {
        stage('Build') {
            agent {
                label 'ec2_agent'
            }
            steps {
                sh 'sed -e "s/%%/$MESSAGE/g" -i index.html'
                sh '''
                #!/bin/bash
                export VERSION=$(git rev-parse --short HEAD)
                docker compose build
                '''
            }
        }
        stage('Push'){
            agent{
                label 'ec2_agent'
            }
            steps{
                sh '$(aws ecr get-login --no-include-email --region us-east-1)'
                sh '''
                #!/bin/bash
                export VERSION=$(git rev-parse --short HEAD)
                docker compose push
                '''
            }
        }
        // stage('Deploy Image'){
        //    agent{
        //        label 'ec2_agent'
        //    }
        //    steps{
        //        sh'''
        //            docker load < /home/user/frontend_${params.BUILD}.tar
        //            docker load < /home/user/backend_${params.BUILD}.tar
        //        '''
        //     }
        // }
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
