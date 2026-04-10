pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "akilaraamana/capstone_project:latest"
        CONTAINER_NAME = "capstone_project"
        EC2_HOST = "13.234.238.147"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerkey',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push $DOCKER_IMAGE
                    docker logout
                    '''
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@$EC2_HOST "
                    docker pull $DOCKER_IMAGE &&
                    docker stop $CONTAINER_NAME || true &&
                    docker rm $CONTAINER_NAME || true &&
                    docker run -d -p 5000:5000 --name $CONTAINER_NAME $DOCKER_IMAGE
                    "
                    '''
                }
            }
        }

        stage('Test Application') {
            steps {
                sh '''
                echo "Waiting for app to start..."
                sleep 10
                curl -f http://$EC2_HOST:5000 || exit 1
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
