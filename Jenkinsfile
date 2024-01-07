pipeline {
    agent any

    stages {
        stage('Deploy to Linux Machine') {
            steps {
                script {
                    withCredentials([
                        usernamePassword(credentialsId: 'vm-credentials', usernameVariable: 'VM_USERNAME', passwordVariable: 'VM_PASSWORD'),
                        usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')
                    ]) {
                        sh """
                            sshpass -p '$VM_PASSWORD' ssh -v -o StrictHostKeyChecking=no $VM_USERNAME@20.127.158.238 << 'ENDSSH'
                                echo "hello"
                                whoami
                                docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD
                                docker stop your_python_project_container || true
                                docker rm your_python_project_container || true
                                docker pull jay899/hello-world:latest
                                docker run -d -p 8080:80 --name your_python_project_container jay899/hello-world:latest
                            
                        """
                    }
                }
            }
        }
    }
}
