pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'httpd-custom'
        DOCKER_TAG = 'latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/HarishBapat/jenkins_demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    sh "docker run -d -p 8080:80 --name httpd-container ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
            sh "docker ps"
        }
    }
}
