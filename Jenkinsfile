pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    // SSH into the target Linux machine and deploy the Docker container
                    sshagent(['your-ssh-key-credential-id']) {
                        // Update 'your_username' and 'your_target_machine_ip' accordingly
                        sh """
                            ssh your_username@your_target_machine_ip << 'ENDSSH'
                                docker stop your_python_project_container || true
                                docker rm your_python_project_container || true
                                docker pull your_username/your_python_project:latest
                                docker run -d -p 8080:80 --name your_python_project_container your_username/your_python_project:latest
                            ENDSSH
                        """
                    }
                }
            }
        }
    }
}
