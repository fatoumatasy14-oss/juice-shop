# Examen final — Sécurité des données
## Évaluation de sécurité OWASP Juice Shop

Projet réalisé dans le cadre de l'examen final du cours Sécurité des données (L3 Cybersécurité).

## Comment exécuter le projet

1. Cloner ce dépôt : `git clone https://github.com/fatoumatasy14-oss/juice-shop.git`
2. Installer les dépendances : `npm install`
3. Lancer l'application : `npm start`
4. Accéder à l'application : http://localhost:3000

## Comment lancer les analyses de sécurité

Le pipeline Jenkins exécute automatiquement les analyses à chaque build :
- **SAST (Semgrep)** : `semgrep scan --config auto --sarif --output semgrep-report.sarif .`
- **SCA (npm audit)** : `npm audit --json > npm-audit-report.json`

Pour lancer manuellement en local :
