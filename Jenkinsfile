pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION    = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Terraform Init') {
            steps {
                dir('terraform') { sh 'terraform init' }
            }
        }
        stage('Terraform Plan') {
            steps {
                dir('terraform') { sh 'terraform plan -out=tfplan' }
            }
        }
        stage('Terraform Apply') {
            steps {
                dir('terraform') { sh 'terraform apply -auto-approve tfplan' }
            }
        }
        stage('Show EC2 IP') {
            steps {
                dir('terraform') { sh 'terraform output ec2_public_ip' }
            }
        }
    }
}