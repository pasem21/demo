pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                aws ecr get-login-password --region us-east-1 | sudo docker login --username AWS --password-stdin 730335381673.dkr.ecr.us-east-1.amazonaws.com
                sudo docker build -t 730335381673.dkr.ecr.us-east-1.amazonaws.com/demo:latest .
                sudo docker push 730335381673.dkr.ecr.us-east-1.amazonaws.com/demo:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                kubectl create ns dev
                helm upgrade -i static-dev -n dev
                '''
            }
        }
    }
}
