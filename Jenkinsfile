pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/JayBroe/Python-playground.git']]])
                git branch: 'main', url: 'https://github.com/JayBroe/test_reporostory.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'python3 classes.py'
            }
        }

        
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
    }
}




