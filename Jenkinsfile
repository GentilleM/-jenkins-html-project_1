
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Downloading HTML source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Checking HTML project files'
                sh 'ls -la'
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t jenkins-html-project_1 .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying HTML application'
                sh 'docker rm -f my-html-container || true'
                sh 'docker run -d -p 5001:80 --name my-html-container jenkins-html-project_1'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed. Check the console output.'
        }
    }
}