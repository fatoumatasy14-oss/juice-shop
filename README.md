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
semgrep scan --config auto --sarif --output semgrep-report.sarif .
npm audit

## Outils utilisés

| Outil | Type | Rôle |
|---|---|---|
| Semgrep | SAST | Analyse statique du code source |
| npm audit | SCA | Analyse des dépendances vulnérables |
| Jenkins | CI/CD | Automatisation du pipeline de sécurité |

## Structure du dépôt

- `Jenkinsfile` — pipeline d'intégration continue à 6 étapes
- `reports/` — rapports générés (Semgrep SARIF, npm audit JSON)
- `screenshots/` — captures d'écran des tests et du pipeline
- `security-config/` — configuration des outils de sécurité
- `remediation/` — détail des corrections appliquées
