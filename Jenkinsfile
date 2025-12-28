pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Aman-ux-source/amazon-clone.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t amanuxsource/amazon-clone:latest .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push amanuxsource/amazonclone:latest'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
