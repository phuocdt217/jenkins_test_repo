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
        stage('Remove') {
            steps {
                sh """
                docker rm -f harbor-image-test
                """
            }
        }
    }
}