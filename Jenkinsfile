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
                    sh('echo $PASSWORD | docker login harbor.nobisoft.com.vn -u $USERNAME --password-stdin')
                    
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

        stage('SSH and Run Docker') {
            steps {
                sshagent(['management-vm']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no root@14.9.0.32 << 'ENDOFSSH'
                        docker pull harbor.nobisoft.com.vn/constellation/harbor-image-test
                        docker stop harbor-image-test || true
                        docker rm harbor-image-test || true
                        docker run --name harbor-image-test -d -p 9980:8000 harbor.nobisoft.com.vn/constellation/harbor-image-test
                        docker ps | grep harbor-image-test
                        'ENDOFSSH' 
                    """
                }
            }
        }
    }
}