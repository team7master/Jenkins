Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any
    stages {
        stage ('Add sudo user') {
            steps {
                sh 'useradd notroot'
            }
       }
        stage ('Privileges to sudoers file') {
            steps {
                sh 'echo "notroot  ALL=(ALL) NOPASSWD:  ALL" >> /etc/sudoers'
                sh 'cat /etc/sudoers >> report.txt'
            }
        }
        stage ('Update the OS with new user') {
            steps {
                sh '''
                    su - 'notroot'
                    yum update -y
                '''          
            }//steps
        }//stage
    }//stages
}//pipeline   '''
            
post {
    always {
        sh '''
            userdel 'notroot' -r
            tail '/etc/sudoers' >> 'report.txt'
        '''
    }//always
}//post
