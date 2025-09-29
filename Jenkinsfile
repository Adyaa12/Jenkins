pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Adyaa12/Jenkins'
            }
        }
        stage('Build') {
            steps{
                sh 'echo "Installing dependencies..."'
                sh 'pip install -r requirements.txt || true'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Running app..."'
                sh 'python3 app.py'
            }
        }
        stage ('Deploy') {
            steps {
                sh 'echo "Deployment step (dummy)"'
            }
        }
    }
}
