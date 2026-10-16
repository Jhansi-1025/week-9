pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                bat "docker build -t jhansirani123/myapp:testimage ."
            }
        }

        stage('Docker Login') {
            steps {
                bat "docker login -u jhansirani123"
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "Pushing Docker Image to Docker Hub"
                bat "docker push jhansirani123/myapp:testimage"
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }
        stage('Verify Deployment') {
            steps {
                bat "kubectl rollout status deployment/kubedemoapp-deployment"
                bat "kubectl get pods -o wide"
                bat "kubectl get svc kubedemoapp-service"
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
