pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Téléchargement du projet'
            }
        }

        stage('Scan SAST Semgrep') {
            steps {
                bat '''
                echo ==========================
                echo Version Semgrep
                echo ==========================

                C:\\Users\\PC LENOVO\\AppData\\Roaming\\Python\\Python313\\Scripts\\semgrep.exe --version

                echo ==========================
                echo Scan de sécurité Semgrep
                echo ==========================

                C:\\Users\\PC LENOVO\\AppData\\Roaming\\Python\\Python313\\Scripts\\semgrep.exe --config auto .

                echo ==========================
                echo Scan terminé
                echo ==========================
                '''
            }
        }

    }
}
