# Configuration des outils de sécurité

## Semgrep (SAST)

Commande utilisée dans le pipeline :
semgrep sc
an --config auto --sarif --output semgrep-report.sarif .


- `--config auto` : sélectionne automatiquement un ensemble de règles adapté au langage détecté (JavaScript/TypeScript pour Juice Shop)
- `--sarif` : génère le rapport au format SARIF (Static Analysis Results Interchange Format), standard reconnu par la plupart des outils d'intégration
- Ruleset : jeu de règles communautaires Semgrep (1074 règles chargées, 307 effectivement appliquées au projet)

## npm audit (SCA)

Commande utilisée dans le pipeline :

npm audit --json > npm-audit-report.json

- Analyse toutes les dépendances déclarées dans `package.json` / `package-lock.json`
- Compare avec la base de données de vulnérabilités connues (CVE) du registre npm
- Sortie au format JSON pour archivage et traitement automatisé

## Résultats obtenus

| Outil | Résultat |
|---|---|
| Semgrep | 51 findings sur 307 règles appliquées |
| npm audit | 52 vulnérabilités (3 low, 18 moderate, 24 high, 7 critical) |
