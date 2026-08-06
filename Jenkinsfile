pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Téléchargement du projet'
            }
        }


        stage('Analyse SAST Semgrep') {

            steps {

                bat '''
                echo ==========================
                echo Version Semgrep
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --version


                echo ==========================
                echo Scan de sécurité Semgrep
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --config auto .


                echo ==========================
                echo Analyse terminée
                echo ==========================
                '''
            }
        }


        stage('Archivage rapport Semgrep') {

            steps {

                archiveArtifacts artifacts: '**/*.sarif',
                fingerprint: true

            }
        }
    }
}