pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "akilaraamana/capstone_project:latest"
        CONTAINER_NAME = "capstone_project"
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

        stage('Deploy') {
            steps {
                sh '''
                docker pull akilaraamana/capstone_project:latest
                docker stop capstone_project || true
                docker rm capstone_project || true
                docker run -d -p 5000:5000 --name capstone_project akilaraamana/capstone_project:latest
                '''
            }
        }
       stage('Test Application') {
    steps {
        sh '''
        sleep 5
        curl -f http://localhost:5000 || exit 1
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
