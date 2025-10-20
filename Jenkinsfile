pipeline {
    agent {
        // Jenkins uruchomi build w oficjalnym kontenerze Python 3.10
        docker { image 'python:3.10' }
    }

    environment {
        // katalog na wyniki testów
        VENV_DIR = 'venv'
    }

    stages {
        stage('Prepare environment') {
            steps {
                echo '🛠 Tworzenie środowiska virtualenv...'
                sh '''
                    python -m venv $VENV_DIR
                    . $VENV_DIR/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                echo '🔍 Sprawdzanie jakości kodu...'
                sh '''
                    . $VENV_DIR/bin/activate
                    flake8 . || true
                '''
            }
        }

        stage('Run tests') {
            steps {
                echo '🧪 Uruchamianie testów z pokryciem kodu...'
                sh '''
                    . $VENV_DIR/bin/activate
                    pytest --cov=. --cov-report=xml --cov-report=term-missing
                '''
            }
        }

        stage('Publish coverage') {
            steps {
                echo '📊 Zapisywanie raportu pokrycia testów...'
                // Jenkins automatycznie zaciągnie plik coverage.xml jako artefakt
                junit 'reports/*.xml'  // tylko jeśli masz raport JUnit — opcjonalne
            }
            post {
                always {
                    archiveArtifacts artifacts: 'coverage.xml', onlyIfSuccessful: true
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline zakończony sukcesem!'
        }
        failure {
            echo '❌ Pipeline nie przeszedł — sprawdź logi w Jenkinsie.'
        }
    }
}
