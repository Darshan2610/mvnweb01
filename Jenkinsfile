pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/darshan2610/mvn01.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Deploy') {
            steps {
                  sh 'mvn clean package'
               ansiblePlaybook playbook: 'ansible/deploy.yml', inventory: 'ansible/hosts.ini'
          
            }
        }
    }
}
