pipeline {
    agent any

    stages {
        
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JayBroe/test_reporostory.git'
            }
        }

        
        stage('Build') {
            steps {
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

