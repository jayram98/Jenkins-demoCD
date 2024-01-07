pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    // Update 'your_username', 'your_password', and 'your_target_machine_ip' accordingly
                    sh """
                        sshpass -p 'your_password' ssh your_username@your_target_machine_ip << 'ENDSSH'
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
