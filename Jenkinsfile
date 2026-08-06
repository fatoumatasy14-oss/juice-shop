pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Téléchargement du projet'
            }
        }

        stage('Semgrep SAST Scan') {
            steps {
                bat '''
                echo ==========================
                echo Version Semgrep
                semgrep --version

                echo ==========================
                echo Scan de sécurité
                semgrep --config auto .
                '''
            }
        }

    }
}