pipeline {
    agent any
    stages {
        stage ('Add sudo user') {
            steps {
                sh """
                   'sh label: '', script: 'useradd notroot'
                   'sh label: '', script: 'echo "password" | passwd --stdin testuser'
                   'sh label: '', script: 'tail /etc/passwd > report.txt'
                """
            }
          }
        stage (Privileges to sudoers file) {
            steps {
                sh """
                   'sh label: '', script: '''echo "notroot  ALL=(ALL) NOPASSWD:  ALL" >> /etc/sudoers
'''
                   'sh label: '', script: 'cat /etc/sudoers >> report.txt'
                """
            }
          }
        stage ('Update the OS with new user') {
            steps {
                sh """
                   sh label: '', script: 'su - notroot'
                   sh label: '', script: 'yum update -y'
                """
            }
          }
        stage ('Remove the sudo user') {
            steps {
                sh """
                   sh label: '', script: 'userdel notroot -r'
                   sh label: '', script: 'tail /etc/sudoers >> report.txt'
            }//steps
        }//stage
    }//stages
}//pipeline
