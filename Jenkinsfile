stage('Analyse SAST Semgrep') {
    steps {
        bat '''
        echo ==========================
        echo Version Semgrep
        echo ==========================

        "C:\\Users\\PC LENOVO\\AppData\\Roaming\\Python\\Python313\\Scripts\\semgrep.exe" --version

        echo ==========================
        echo Scan de sécurité Semgrep
        echo ==========================

        "C:\\Users\\PC LENOVO\\AppData\\Roaming\\Python\\Python313\\Scripts\\semgrep.exe" --config auto .

        echo ==========================
        echo Analyse terminée
        echo ==========================
        '''
    }
}