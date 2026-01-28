pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Code checked out"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest app/'
            }
        }

        stage('Deploy to DEV') {
            steps {
                sh 'kubectl apply -f k8s/dev/'
            }
        }

        stage('Approve QA') {
            steps {
                input "Deploy to QA?"
            }
        }

        stage('Deploy to QA') {
            steps {
                sh 'kubectl apply -f k8s/qa/'
            }
        }

        stage('Approve PROD') {
            steps {
                input "Deploy to PROD?"
            }
        }

        stage('Deploy to PROD') {
            steps {
                sh 'kubectl apply -f k8s/prod/'
            }
        }
    }
}
