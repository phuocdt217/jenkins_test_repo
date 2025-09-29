pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh """
                docker build -f docker/Dockerfile -t harbor-image-test .
                """
            }
        }
        stage('Run') {
            steps {
                sh """
                docker run -p 8080:8000 harbor-image-test
                """
            }
        }
    }
}