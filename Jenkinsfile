pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/JayBroe/Python-playground.git']]])
            }
        }
        
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/JayBroe/Python-playground.git'
                sh 'python3 classes.py'
            }
        }

        
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }

         post {
        success {
            echo '✅ Build zakończony sukcesem!'
        }
        failure {
            echo '❌ Błąd podczas builda.'
        }
    }

    }
}







