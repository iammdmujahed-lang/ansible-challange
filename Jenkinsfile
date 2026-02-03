pipeline {
    agent any
    environment {
        AWS_CREDENTIALS = credentials('aws-keys')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Terraform Apply') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-keys', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh 'terraform init'
                    sh 'terraform apply -auto-approve' // Remove the citation tag here
                }
            }
        }
        stage('Ansible Deploy') {
            steps {
                sleep 30 
                sh 'ansible-playbook -i inventory.ini setup.yml'
            }
        }
    }
}
