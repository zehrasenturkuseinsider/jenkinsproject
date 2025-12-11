pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/zehrasenturkuseinsider/jenkinsproject.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install pytest pytest-html
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest --junitxml=report.xml --html=report.html
                    python3 hello.py
                '''
            }
        }
    }

    post {
        always {
            junit 'report.xml'
            publishHTML(target: [
                reportDir: '.',
                reportFiles: 'report.html',
