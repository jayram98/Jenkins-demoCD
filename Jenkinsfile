pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    // Define credentials IDs for SSH and Docker
                    def sshCredentialsId = 'ssh-credentials'
                    def dockerCredentialsId = 'docker-credentials'

                    // Use withCredentials for both Docker and SSH
                    withCredentials([
                        usernamePassword(credentialsId: dockerCredentialsId, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD'),
                        usernamePassword(credentialsId: sshCredentialsId, usernameVariable: 'VM_USERNAME', passwordVariable: 'VM_PASSWORD')
                    ]) {
                        sh """
                            sshpass -p '$VM_PASSWORD' ssh -o StrictHostKeyChecking=no $VM_USERNAME@20.127.158.238 bash -s << 'ENDSSH'
                                docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                                docker stop your_python_project_container || true
                                docker rm your_python_project_container || true
                                docker pull your_docker_username/your_python_project:latest
                                docker run -d -p 8080:80 --name your_python_project_container your_docker_username/your_python_project:latest
                            ENDSSH
                        """
                    }
                }
            }
        }
    }
}
