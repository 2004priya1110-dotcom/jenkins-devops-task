pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-devops-task'
        CONTAINER_NAME = 'jenkins-devops-task-container'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Docker image...'
                bat 'docker run --rm %IMAGE_NAME% nginx -t'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                bat 'docker rm -f %CONTAINER_NAME% 2>NUL || exit /b 0'

                bat 'docker run -d --name %CONTAINER_NAME% -p 8081:80 %IMAGE_NAME%'
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
