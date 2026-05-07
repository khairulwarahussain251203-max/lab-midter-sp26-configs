pipeline {
    agent any
    stages {
        stage('Fetch Data from GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/khairulwarahussain251203-max/lab-midter-sp26-configs.git'
            }
        }
        stage('Train Model') {
            steps {
                sh 'pip install -r requirements.txt --break-system-packages'
                sh 'python3 train.py'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ml-fastapi-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop ml-container || true
                    docker rm ml-container || true
                    docker run -d -p 8000:8000 --name ml-container ml-fastapi-app
                '''
            }
        }
    }
}
