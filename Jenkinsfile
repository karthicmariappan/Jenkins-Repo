pipeline {
    agent any

    environment {
        IMAGE_NAME = 'karthickm13799/jenkins-image'
        TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout ([$class: 'GitSCM',
                           branches: [[name: '*/main']],
                           userRemoteconfigs: [[
                               url:'https://github.com/karthicmariappan/Jenkins-Repo.git'
                           ]]
                ])
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${TAG} ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}:${TAG}"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker image pushed successfully!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
