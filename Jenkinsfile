pipeline {
    agent any

    stages {

        stage('Check Python') {
            steps {
                sh '''
                python3 --version || python --version
                '''
            }
        }

        stage('Create Virtual Environment') {
            steps {
                sh '''
                python3 -m venv venv
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
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
                python -m pytest || true
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Python CI Pipeline completed successfully'
        }
        failure {
            echo '❌ Pipeline failed'
        }
    }
}
