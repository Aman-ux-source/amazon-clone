pipeline {
    agent any

    environment {
        IMAGE = "amanuxsource/amazon-clone"
    }

    stages{
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

        stage('Push Image to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push $IMAGE:latest"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f amazonclone || true
                    docker run -d --name amazonclone -p 8080:80 amanuxsource/amazon-clone:latest
                '''
            }
        }
    }
}
