pipeline {
    agent any

    stages {
        
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JayBroe/test_reporostory.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Run tests') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm run build'
                sh 'python3 ops.py'
            }
        }

        
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
    }
}
