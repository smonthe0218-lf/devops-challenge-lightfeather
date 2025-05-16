pipeline {
  agent any
  environment {
    AWS_ACCESS_KEY_ID = credentials('accesskeyid')      
    AWS_SECRET_ACCESS_KEY = credentials('accesskey')  
  }
  stages {
    stage('Checkout the code') {
      steps {
        git branch: 'main', credentialsId: 'github-id', url: 'https://github.com/smonthe0218-lf/devops-coding-challenge.git'
        sh 'ls -l'
      }
    }
    stage('Terraform init') {
      steps {
        withEnv([
OAOAOA          "AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}",
          "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}",
          "AWS_DEFAULT_REGION=us-east-1"
        ]) {
          sh 'terraform init -backend-config=backend/devops.tf'
        }
      }
    }
    stage('Terraform plan') {
      steps {
        withEnv([
          "AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}",
          "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}",
          "AWS_DEFAULT_REGION=us-east-1"
        ]) {
          sh 'terraform plan -var-file vars/devops.tfvars'
        }
      }
    }
    stage('Terraform apply') {
      steps {
        withEnv([
          "AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}",
          "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}",
          "AWS_DEFAULT_REGION=us-east-1"
        ]) {
          sh 'terraform apply -var-file vars/devops.tfvars -auto-approve'
        }
      }
    }
  }
}
