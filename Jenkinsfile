pipeline {
    agent none
    parameters {
        string(name: 'MESSAGE', defaultValue: 'Hello World!', description: 'Title')
    }
    stages {
        stage('Build Image') {
            agent {
                label 'ec2_agent'
            }
            steps {
                sh "docker version"
                sh "docker compose version"
            }
        }
        // stage('Push Image'){
        //     agent{
        //         label 'ec2_agent'
        //     } 
        //     steps{
        //         sh'''
        //             scp ./frontend_${params.BUILD}.tar user@proddocker01:/home/user/
        //             scp ./backend_${params.BUILD}.tar user@proddocker01:/home/user/
        //         '''
        //      }   
        // }
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
