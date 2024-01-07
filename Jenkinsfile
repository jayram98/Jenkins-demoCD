pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'vm-credentials', usernameVariable: 'VM_USERNAME', passwordVariable: 'VM_PASSWORD')]) {
                        sh """
                            sshpass -p '$VM_PASSWORD' ssh -v -o StrictHostKeyChecking=no $VM_USERNAME@20.127.158.238 << 'ENDSSH'
                                echo "hello"
                                whoami
                                docker stop jay899/hello-world || true
                                docker rm jay899/hello-world || true
                                docker pull your_jay899/hello-world:latest
                                docker run -d -p 8080:80 --name your_python_project_container jay899/hello-world:latest
                            ENDSSH
                        """
                    }
                }
            }
        }
    }
}
