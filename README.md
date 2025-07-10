


pipeline {
    agent any

    stages {

        stage('Install Git and Clone Repo') {
            steps {
                sh 'sudo apt-get update && sudo apt-get install -y git'
                git branch: 'main', url: 'https://github.com/Vinayak-100ni/terraform-eks.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }

    }

    post {
        failure {
            echo '❌ Pipeline failed.'
        }
        success {
            echo '✅ Pipeline completed successfully.'
        }
    }
}
