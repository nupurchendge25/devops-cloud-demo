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
        echo 'Deploying application to EC2...'

        sshagent(['ec2-ssh']) {
            sh '''
                scp -o StrictHostKeyChecking=no devops-cloud-demo.tar.gz ubuntu@51.21.199.234:/tmp/

                ssh -o StrictHostKeyChecking=no ubuntu@51.21.199.234 "
                    sudo rm -rf /var/www/html/*
                    sudo tar -xzf /tmp/devops-cloud-demo.tar.gz -C /var/www/html
                    sudo systemctl reload nginx
                "
            '''
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
