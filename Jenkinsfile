pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'vm-credentials', usernameVariable: 'VM_USERNAME', passwordVariable: 'VM_PASSWORD')]) {
                        sh """
                            sshpass -p '$VM_PASSWORD' ssh -o StrictHostKeyChecking=no $VM_USERNAME@20.127.158.238 bash -s << 'ENDSSH'
                                echo "hello"
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
