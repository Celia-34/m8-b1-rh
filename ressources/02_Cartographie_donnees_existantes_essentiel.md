# Cartographier les données (existantes vs à acquérir) — Mini-cours

> Brief associé : M8-B1
> Durée de lecture : ~20 min
> Pré-requis : entretien mené

## Pourquoi cette techno ?

Un projet IA vit ou meurt sur ses **données**. Avant de parler modèle, il faut
savoir ce que le client a **déjà** (exploitable tout de suite) et ce qui **manque**
(à collecter, à acheter, ou bloquant). Cette cartographie évite de promettre une
solution impossible (« on prédit X » alors que les données de X n'existent pas) et
révèle le **vrai coût** caché du projet (acquisition de données).

## Concepts clés

- **Existantes vs à acquérir** : deux colonnes distinctes. Les existantes
  conditionnent un POC rapide ; les à acquérir conditionnent le délai et le budget.
- **Qualité estimée à l'œil** : volume, fraîcheur, complétude, présence
  d'**annotations/labels** (crucial pour du supervisé).
- **Contraintes d'accès** : qui détient la donnée, sous quel format, avec quelle
  base légale, où elle est stockée.
- **Labels = or** : un dataset **déjà catégorisé** (ex. tickets RH historiques)
  change tout — il rend le supervisé possible sans annotation coûteuse.
- **Points à clarifier** : lister ce qu'on ne sait pas encore (à confirmer avec le
  client) plutôt que de supposer.

## Exemple minimal qui tourne

```markdown
| Donnée | Statut | Qualité | Remarque |
|---|---|---|---|
| 10k tickets catégorisés | existante | bonne | dataset labellisé |
| Texte des tickets | existante | variable | PII présentes |
| Comptes-rendus PDF | à acquérir | ? | hors périmètre v1 |
```

## Exercice guidé

Pour ton cas :
1. Liste les données **existantes** révélées en entretien + leur qualité estimée.
2. Liste ce qui **manque** pour répondre au besoin.
3. Y a-t-il des **labels** exploitables ? (change la faisabilité du supervisé)

## Pièges fréquents

| Piège | Conséquence |
|---|---|
| Mélanger existant et à acquérir | On surestime la faisabilité immédiate |
| Oublier les labels | On rate la possibilité d'un supervisé simple |
| Supposer la qualité | Mauvaise surprise au POC |
| Ignorer les contraintes d'accès | Projet bloqué par le RGPD / la propriété |

| Symptôme | Cause probable |
|---|---|
| « On prédira X » mais X n'a pas de données | pas de cartographie sérieuse |
| Délai sous-estimé | données « à acquérir » non identifiées |
| Modèle supervisé impossible | absence de labels non repérée |

## Pour aller plus loin

- Cf. mini-cours M3-B1 (cartographie de sources) — capitalisation.
- CNIL — minimisation des données : https://www.cnil.fr/fr/intelligence-artificielle/ia-comment-etre-en-conformite-avec-le-rgpd

## Vérification (checklist apprenant)

- [ ] Deux colonnes distinctes (existantes / à acquérir).
- [ ] Qualité estimée par source.
- [ ] Présence (ou non) de **labels** identifiée.
- [ ] Contraintes d'accès notées.
- [ ] Points à clarifier listés (pas supposés).

> 💡 **Récap — Cartographie données** : séparer **existantes** (POC immédiat) et **à acquérir** (délai/budget caché) ; estimer la qualité à l'œil ; repérer les **labels** (rendent le supervisé possible) ; noter les contraintes d'accès. Un projet IA vit ou meurt sur ses données.

### À retenir

- Le livrable se juge sur sa **clarté pour le destinataire**, pas sur sa longueur.
- **Chiffrer** plutôt qu'affirmer : un nombre vaut mieux qu'un adjectif.
- **Sobriété** : recommander le plus simple qui résout le besoin, et **dire ce qu'on écarte**.
- Distinguer ce qu'on **sait** de ce qui reste **à clarifier** (questions ouvertes).
- Tracer ses **choix** et leur **raison** — c'est ce qui se défend en restitution.
