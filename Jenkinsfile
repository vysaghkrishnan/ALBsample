pipeline {
    agent any

    environment {
  registry  = "public.ecr.aws/dockerlb"
}
    stages {
        stage ('Checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitHUB', url: 'https://github.com/vysaghkrishnan/ALBsample.git']]])
            }
        }
        stage ('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        stage ('Docker Push') {
            steps {
                script {
                    sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/j6w0n6r7'
                    sh 'docker push public.ecr.aws/j6w0n6r7/public.ecr.aws/dockerlb:latest'
                }
           }
        }
    }
}
