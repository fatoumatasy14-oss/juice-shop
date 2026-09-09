pipeline {
  agent any

  environment {
    SEMGREP = 'C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe'
  }

  stages {
    stage('Checkout') {
      steps {
        echo 'Telechargement du projet depuis GitHub'
        checkout scm
      }
    }

    stage('Build / Preparation') {
      steps {
        echo 'Installation des dependances du projet'
        bat 'npm install --no-audit --prefer-offline'
      }
    }

    stage('Security Analysis - SAST (Semgrep)') {
      steps {
        echo 'Analyse statique du code avec Semgrep'
        powershell '''
$env:PYTHONUTF8 = "1"
$env:PYTHONIOENCODING = "utf-8"
& "C:\\Users\\PC LENOVO\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\semgrep.exe" scan --config auto --sarif --output semgrep-report.sarif .
'''
      }
    }

    stage('Additional Security Check - SCA (npm audit)') {
      steps {
        echo 'Analyse des dependances avec npm audit'
        bat 'npm audit --json > npm-audit-report.json || exit 0'
      }
    }

    stage('Report Generation') {
      steps {
        echo 'Archivage des rapports de securite'
        archiveArtifacts artifacts: 'semgrep-report.sarif, npm-audit-report.json', fingerprint: true
      }
    }

    stage('Notification') {
      steps {
        echo 'Envoi du rapport par e-mail'
        emailext (
          subject: "Resultat du build ${env.JOB_NAME} #${env.BUILD_NUMBER}: ${currentBuild.currentResult}",
          body: "Le pipeline de securite s'est termine avec le statut ${currentBuild.currentResult}. Rapports en piece jointe.",
          to: 'fatoumata.sy14@unchk.edu.sn',
          attachmentsPattern: 'semgrep-report.sarif, npm-audit-report.json'
        )
      }
    }
  }
}
