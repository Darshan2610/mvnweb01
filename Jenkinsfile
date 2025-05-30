
pipeline {
    agent any

    tools {
        maven 'maven' // Must match the name configured in Jenkins global tools
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Darshan2610/mvnwebapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive WAR') {
            steps {
                // Archive the exact WAR file name, assuming it's MyMavenWebApp.war
                archiveArtifacts artifacts: 'target/MyMavenWebApp.war', fingerprint: true
            }
        }

        stage('Deploy with Ansible') {
            steps {
                // Run deployment using Ansible (ensure Jenkins has Ansible plugin + rights)
                ansiblePlaybook playbook: 'ansible/deploy.yml', inventory: 'ansible/hosts.ini'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
