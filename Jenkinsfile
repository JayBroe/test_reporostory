pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pobiera kod z repo (możesz zmienić na własne)
                git branch: 'main', url: 'https://github.com/JayBroe/test_reporostory.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                sh 'flake8 . || true'
            }
        }

        stage('Run tests') {
            steps {
                sh 'pytest -v'
            }
        }
    }

    post {
        success {
            echo '✅ Wszystkie testy zakończone sukcesem!'
        }
        failure {
            echo '❌ Błąd podczas budowania lub testów!'
        }
    }

}
