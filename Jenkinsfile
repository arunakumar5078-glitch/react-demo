pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t react-demo:%BUILD_NUMBER% -t react-demo:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker rm -f react-demo || exit 0'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 3000:80 --name react-demo react-demo:latest'
            }
        }
    }

    post {
        success {
            echo 'Done! Open http://localhost:3000'
        }
        failure {
            echo 'Build failed. Check the console output.'
        }
    }
}
