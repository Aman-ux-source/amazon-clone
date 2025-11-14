pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('6f1f115c-6dc3-403b-a16c-c45bc86ec4fb')
        IMAGE = "Amanuxsource/amazon-clone"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Aman-ux-source/amazon-clone.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE:latest ."
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh "echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin"
                sh "docker push $IMAGE:latest"
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f amazon || true
                    docker run -d --name amazon -p 8080:80 $IMAGE:latest
                '''
            }
        }
    }
}

