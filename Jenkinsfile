pipeline {
    agent any

    environment {
        KUBECONFIG = "C:\\ProgramData\\Jenkins\\.jenkins\\.kube\\config"
        MINIKUBE_HOME = "C:\\ProgramData\\Jenkins\\.jenkins\\.minikube"
    }

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

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml --validate=false'
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