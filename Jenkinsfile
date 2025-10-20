pipeline {
    agent any

    stages {
        stage('Setup Python') {
            steps {
                sh '''
                apt-get update
                apt-get install -y python3 python3-pip python3-venv
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                . venv/bin/activate
                pytest --cov=. --cov-report=term-missing
                '''
            }
        }
    }
}

