pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo"
        IMAGE_TAG = "v1"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/saitejareddy05/jenkins-docker-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8080:80 ${IMAGE_NAME}:${IMAGE_TAG}'
            }
        }
    }

    post {
        success {
            emailext (
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build succeeded! Check logs at ${env.BUILD_URL}",
                to: "saitejareddy0126@gmail.com"
            )
        }
        failure {
            emailext (
                subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed. Please check the logs: ${env.BUILD_URL}",
                to: "saitejareddy0126@gmail.com"
            )
        }
    }
}
