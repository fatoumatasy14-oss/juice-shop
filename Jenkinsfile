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
                @echo off

                REM ==========================
                REM Encodage UTF-8
                REM ==========================
                chcp 65001 > nul
                set PYTHONUTF8=1
                set PYTHONIOENCODING=utf-8

                echo ==========================
                echo Version Semgrep
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --version

                echo.
                echo ==========================
                echo Analyse Semgrep (JSON)
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --config auto --json --output semgrep-report.json .

                echo.
                echo ==========================
                echo Analyse Semgrep (SARIF)
                echo ==========================

                "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" --config auto --sarif --output semgrep-report.sarif . || echo Erreur SARIF ignoree

                echo.
                echo ==========================
                echo Rapports generes
                echo ==========================

                dir semgrep-report.*

                echo.
                echo ==========================
                echo Analyse terminee
                echo ==========================
                '''
            }
        }

        stage('Archivage des rapports') {
            steps {
                archiveArtifacts artifacts: 'semgrep-report.*', fingerprint: true, allowEmptyArchive: true
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