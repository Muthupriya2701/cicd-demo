pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source Code Checkout Completed'
            }
        }

        stage('Maven Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t cicd-demo:latest .'
            }
        }

        stage('Load Image to Minikube') {
            steps {
                bat 'minikube image load cicd-demo:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get pods'
            }
        }
    }

    post {
        success {
            echo 'Pipeline Completed Successfully!'
        }
        failure {
            echo 'Pipeline Failed! Check Logs.'
        }
    }
}