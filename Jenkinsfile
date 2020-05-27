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
            }
          }
        stage ('Remove the sudo user') {
            steps {
                sh '''
                    userdel 'notroot' -r
                    tail '/etc/sudoers' >> 'report.txt'
                '''
            }//steps
        }//stage
    }//stages
}//pipeline
