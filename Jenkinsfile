pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "spring-petclinic-bar"
    }

    stages {
        stage('Compile') {
            steps {
                echo 'Compiling the code...'
                sh './mvnw compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh './mvnw test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging project to JAR...'
                sh './mvnw package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${DOCKER_IMAGE}:${env.BUILD_ID} ."
                sh "docker tag ${DOCKER_IMAGE}:${env.BUILD_ID} ${DOCKER_IMAGE}:latest"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs.'
        }
    }
}