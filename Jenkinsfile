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
                sh 'zip -r classes.zip .'
            }
        post {
            success {
                echo '✅ Build zakończony sukcesem!'
        }
            failure {
                echo '❌ Błąd podczas builda. Sprawdź logi.'
        }
    }            
        }

        
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        post {
            success {
                echo '✅ Test zakończony sukcesem!'
        }
            failure {
                echo '❌ Błąd podczas testu. Sprawdź logi.'
        }
    }            
        }

        stage('Deploy') {
            steps {
                archiveArtifacts artifacts: 'classes.zip', fingerprint: true
            }
        post {
            success {
                echo '✅ Deploy zakończony sukcesem!'
        }
            failure {
                echo '❌ Błąd podczas deployowania. Sprawdź logi.'
        }
    }             
        }      
        }
}







