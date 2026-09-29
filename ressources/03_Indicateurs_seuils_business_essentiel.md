# Indicateurs et seuils business — Mini-cours

> Brief associé : M8-B1
> Durée de lecture : ~20 min
> Pré-requis : besoin métier reformulé

## Pourquoi cette techno ?

Un projet IA n'est **pilotable** que s'il est **mesurable**. « Améliorer le tri »
ne se mesure pas ; « passer de 60 à 10 min/jour avec 85 % des tickets dans la bonne équipe » se mesure.
Définir des **indicateurs business chiffrés** et des **seuils d'acceptabilité**
transforme une intention en objectif vérifiable — et protège le projet contre le
« on verra bien ». C'est aussi l'ancrage de la compétence C8 (mesurer la perf).

## Concepts clés

- **KPI business ≠ métrique modèle** : le KPI parle au client (temps gagné, € de
  panne évités) ; la métrique modèle (F1, recall) est le moyen.
- **Chiffrer** : un KPI a une valeur de départ et une cible (« 60 → 10 min/jour »).
- **Seuil d'acceptabilité** : en dessous, le projet n'a pas de valeur (« moins de
  85 % de bons routages = inexploitable »).
- **Lier KPI et métrique** : « exactitude > 85 % » (modèle) sert le « temps de tri
  divisé par 6 » (business).
- **Nommer la bonne métrique** : l'**exactitude** compte les bonnes décisions sur
  le total (« 85 % des tickets dans la bonne équipe ») ; la **précision** compte,
  parmi les alertes levées, celles qui étaient vraies (« combien de fausses
  alertes ? ») ; le **rappel** compte, parmi les vrais cas, ceux qu'on a
  détectés (« combien de pannes ratées ? »). Un pourcentage sans son nom est
  inutilisable.
- **Anti-magie** : « 95 % » sorti du chapeau ne vaut rien — le seuil se
  justifie par le **coût de l'erreur** (récupérable ? critique ?).
- **Coût de l'erreur** : un faux tri RH est récupérable (seuil souple) ; un faux
  négatif de maintenance coûte 30 k€ (seuil sur le recall plus exigeant).

## Exemple minimal qui tourne

```markdown
| KPI | Cible | Seuil d'acceptabilité |
|---|---|---|
| Temps de tri | 60 → 10 min/jour | ≤ 15 min |
| Exactitude du tri (tickets dans la bonne équipe) | — | > 85 % |
| Taux de revue humaine | — | < 20 % |
```

## Exercice guidé

Pour ton cas :
1. Définis 3 KPI **business** chiffrés (valeur départ → cible).
2. Associe à chacun un **seuil d'acceptabilité**.
3. Justifie un seuil par le **coût de l'erreur** (récupérable vs critique).

## Pièges fréquents

| Piège | Conséquence |
|---|---|
| KPI non chiffré | Projet non pilotable |
| Confondre KPI business et métrique modèle | Le client ne comprend pas |
| Seuil magique (« 95 % ») | Indéfendable, non relié au coût |
| Oublier le coût de l'erreur | Seuil inadapté (trop / pas assez exigeant) |

| Symptôme | Cause probable |
|---|---|
| « Améliorer X » sans chiffre | pas de KPI mesurable |
| Seuil contesté par le client | pas relié au coût métier |
| Métrique modèle seule | manque le KPI business |

## Pour aller plus loin

- Cf. M6-B1 (indicateurs, seuils) — capitalisation côté exploitation.
- scikit-learn — metrics : https://scikit-learn.org/stable/modules/model_evaluation.html

## Vérification (checklist apprenant)

- [ ] 3-5 KPI **business** chiffrés (départ → cible).
- [ ] Un seuil d'acceptabilité par KPI.
- [ ] Distinction KPI business / métrique modèle.
- [ ] Au moins un seuil justifié par le coût de l'erreur.
- [ ] Lisible par le décideur métier.

> 💡 **Récap — Indicateurs business** : chiffrer le KPI **business** (60→10 min), pas juste la métrique modèle ; un seuil d'acceptabilité par KPI, justifié par le **coût de l'erreur** (récupérable vs critique). « 95 % » sorti du chapeau, sans nom de métrique, ne vaut rien.

### À retenir

- Le livrable se juge sur sa **clarté pour le destinataire**, pas sur sa longueur.
- **Chiffrer** plutôt qu'affirmer : un nombre vaut mieux qu'un adjectif.
- **Sobriété** : recommander le plus simple qui résout le besoin, et **dire ce qu'on écarte**.
- Distinguer ce qu'on **sait** de ce qui reste **à clarifier** (questions ouvertes).
- Tracer ses **choix** et leur **raison** — c'est ce qui se défend en restitution.
