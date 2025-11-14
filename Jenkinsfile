pipeline {
    agent any

    environment {
        DOCKERHUB_USER = credentials('Amanuxsource')
        DOCKERHUB_PASS = credentials('Amanpreet#8979')
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

