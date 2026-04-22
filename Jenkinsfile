pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jtapalanivel/html-docker-app.git'
                echo 'Code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t html-app .'
                    echo 'Docker image built successfully'
                }
            }
        }

        stage('Test Container') {
            steps {
                script {
                    sh 'docker run -d --name test-container -p 8081:80 html-app'
                    sh 'timeout 5'
                    sh 'curl -f http://localhost:8081 || exit 1'
                    sh 'docker stop test-container && docker rm test-container'
                    echo 'Container test passed!'
                }
            }
        }

        stage('Push to Registry') {
            steps {
                echo 'Ready to push to Docker Hub or Heroku'
            }
        }
    }

    post {
        success {
            echo '?? Pipeline completed successfully!'
        }
        failure {
            echo '? Pipeline failed. Check the logs.'
        }
    }
}
