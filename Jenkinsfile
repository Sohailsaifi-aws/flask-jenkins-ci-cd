pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-jenkins-app"        
    }
    stages {
        stage(checkout) {
            steps {
                git 'https://github.com/Sohailsaifi-aws/flask-jenkins-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Unit Test') {
            steps {
                sh '''
                docker run --rm $IMAGE-NAME pytest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop flask_app || true
                docker rm flask_app || true
                docker run -d -p 5000:5000 --name flask_app $IMAGE_NAME
                '''
            }
        }
}
post {
    success {
        echo "FLASK CI/CD PIPELINE SUCCESSFUL"
    }
    failure {
        echo "PIPELINE FAILED"
    }
}
}