pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    // Define credentials IDs for SSH and Docker
                    def sshCredentialsId = 'ssh-credentials'
                    def dockerCredentialsId = 'docker-credentials'

                    // Use withCredentials for SSH
                    withCredentials([usernamePassword(credentialsId: sshCredentialsId, usernameVariable: 'VM_USERNAME', passwordVariable: 'VM_PASSWORD')]) {
                        sh """
                            sshpass -p '$VM_PASSWORD' ssh -o StrictHostKeyChecking=no $VM_USERNAME@20.127.158.238 bash -s << 'ENDSSH'
                                docker login -u your_docker_username -p your_docker_password
                                docker stop your_python_project_container || true
                                docker rm your_python_project_container || true
                                docker pull your_docker_username/your_python_project:latest
                                docker run -d -p 8080:80 --name your_python_project_container your_docker_username/your_python_project:latest
                            ENDSSH
                        """
                    }

                    // Use withCredentials for Docker (for pulling the image and login)
                    withCredentials([usernamePassword(credentialsId: dockerCredentialsId, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                            docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                            docker pull your_docker_username/your_python_project:latest
                        """
                    }
                }
            }
        }
    }
}
