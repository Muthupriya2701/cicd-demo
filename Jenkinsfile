pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/YourUsername/springboot-cicd-app.git'
            }
        }

        stage('Maven Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t springboot-app:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
            }
        }

        stage('Verify') {
            steps {
                bat 'kubectl get pods'
            }
        }
    }

    post {
        success {
            echo 'Pipeline Successful!'
        }
        failure {
            echo 'Pipeline Failed!'
        }
    }
}