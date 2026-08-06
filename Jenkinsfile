pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Téléchargement du projet depuis GitHub'
                checkout scm
            }
        }

        stage('Scan SAST Semgrep') {
            steps {
                bat '''
                echo ==========================
                echo Version Semgrep
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --version

                echo ==========================
                echo Analyse Semgrep (JSON)
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --config auto --json --output semgrep-report.json .

                echo ==========================
                echo Analyse Semgrep (SARIF)
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --config auto --sarif --output semgrep-report.sarif .

                echo ==========================
                echo Analyse terminée
                echo ==========================
                '''
            }
        }

        stage('Archivage des rapports') {
            steps {
                archiveArtifacts artifacts: 'semgrep-report.json, semgrep-report.sarif', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build terminé avec succès.'
        }

        failure {
            echo 'Le build a échoué.'
        }

        always {
            echo 'Fin du pipeline Jenkins.'
        }
    }
}