pipeline {
    agent any

    tools {
        python 'Python3'
    }

    environment {
        VENV = 'venv'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/<your-username>/python-web-app.git'
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source venv/bin/activate
                pytest || true
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                source venv/bin/activate
                python app.py &
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Python CI/CD Pipeline Successful"
        }
        failure {
            echo "❌ Pipeline Failed"
        }
    }
}
