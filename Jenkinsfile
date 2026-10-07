pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'test -f index.html'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'grep -q "Hello from Jenkins CD Pipeline!" index.html'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging application...'
                sh 'mkdir -p package'
                sh 'cp index.html package/'
                sh 'tar -czf devops-cloud-demo.tar.gz -C package .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage will be configured after cloud setup.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
