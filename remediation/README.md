# Résumé des remédiations appliquées

Trois vulnérabilités ont été sélectionnées pour remédiation, couvrant l'authentification, la validation des entrées et le contrôle d'accès. Le détail complet (cause, correction, justification, vérification) est disponible dans le rapport principal, section 6.

## V1 — SQL Injection

**Cause :** requête SQL construite par concaténation de chaînes.

**Correction :** utilisation de requêtes paramétrées.
```javascript
// Avant
const query = "SELECT * FROM users WHERE email = '" + email + "'";
// Après
const query = "SELECT * FROM users WHERE email = ?";
db.get(query, [email]);
```

**Vérification :** le payload `' OR 1=1--` ne permet plus de contourner l'authentification.

## V2 — XSS stocké

**Cause :** contenu utilisateur inséré directement en HTML sans encodage.

**Correction :** utilisation de `textContent` au lieu de `innerHTML`.
```javascript
// Avant
element.innerHTML = userReview;
// Après
element.textContent = userReview;
```

**Vérification :** le payload s'affiche désormais comme texte brut, sans exécution du script.

## V3 — IDOR

**Cause :** absence de vérification de propriété de la ressource demandée.

**Correction :** vérification explicite côté serveur.
```javascript
if (!basket || basket.userId !== req.user.id) {
  return res.status(403).send('Accès refusé');
}
```

**Vérification :** l'accès au panier d'un autre utilisateur renvoie désormais une erreur 403.
