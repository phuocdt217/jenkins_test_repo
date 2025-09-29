pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh """
                docker build -f docker/Dockerfile -t harbor.nobisoft.com.vn/constellation/harbor-image-test .
                """
            }
        }

        stage('Login To Harbor') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'harbor_cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                    echo $PASSWORD | docker login harbor.nobisoft.com.vn -u $USERNAME --password-stdin
                    """
                }
            }
        }

        stage('Push Image To Harbor') {
            steps {
                sh """
                docker push harbor.nobisoft.com.vn/constellation/harbor-image-test
                """
            }
        }
    }
}