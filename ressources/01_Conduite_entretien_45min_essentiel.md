# Conduire un entretien client sous contrainte (45 min, 12 réponses) — Mini-cours

> Brief associé : M8-B1
> Durée de lecture : ~25 min
> Pré-requis : aucun (posture consultant)

## Pourquoi cette techno ?

Un client dit rarement ce dont il a **besoin** : il exprime une **demande**
(« on veut de l'IA »). L'entretien de cadrage sert à creuser sous la demande pour
trouver le besoin réel, les données, les contraintes et les critères de succès.
En M8-B1, le client fictif en ligne t'accorde **45 minutes et 12 réponses** :
chaque question compte. Sans préparation, tu dépenses ton budget sur des détails
et tu repars sans l'essentiel. C'est la compétence **la plus exigeante du
parcours sur CT3** (définir le périmètre), et le quotidien du consultant IA.

## Concepts clés

- **Demande ≠ besoin** : « un assistant qui rédige » (demande) cache souvent
  « gagner du temps sans risque » (besoin). On reformule, on ne recopie pas.
- **Budget de questions → priorisation** : prépare 12 questions + 3 de réserve,
  **classées par priorité**. Couvre au moins : besoin, processus actuel, données
  (existence, volume, qualité), données personnelles, critère de succès chiffré,
  coût d'une erreur, utilisateurs, SI / hébergement, budget / délai.
- **Une question à la fois** : « Vous avez des données et quel budget ? » obtient
  **une** réponse et te coûte une question. Une question = un sujet.
- **Ouverte vs fermée** : une question **ouverte** (« Comment se passe le tri
  aujourd'hui ? ») fait émerger ce que tu n'avais pas prévu ; une question
  **fermée** (« Les tickets sont-ils déjà catégorisés ? ») vérifie un point
  précis. Commence ouvert sur le besoin, termine fermé sur les chiffres.
- **Demander un extrait de données** : c'est la question la plus rentable. Un
  échantillon réel vaut dix descriptions (qualité, format, surprises). Le client
  ne l'envoie **que si on le demande**.
- **Relancer** : une réponse surprenante vaut une relance (« vous dites que… ça
  arrive souvent ? »), quitte à sacrifier une question préparée de priorité 3.
- **Question imposée — volumétrie labellisée** : « combien d'exemples, labellisés
  comment ? ». Peu de données + modèle complexe = surapprentissage ; elle
  conditionne l'arbitrage ML/DL de M8-B2.
- **Écoute active** : noter ce qui est **dit** ET ce qu'on **interprète**, séparément.

## Exemple minimal qui tourne

```text
Priorité 1 (besoin)  : Qu'est-ce qui vous fait perdre le plus de temps aujourd'hui ?
Priorité 1 (données) : Avez-vous un historique déjà classé ? Sur combien d'années ?
Priorité 1 (données) : Pouvez-vous m'envoyer un petit extrait ?
Priorité 1 (succès)  : Qu'est-ce qui vous ferait dire que le projet est réussi ?
Priorité 2 (risque)  : Que se passe-t-il si l'outil se trompe ?
Priorité 2 (RGPD)    : Y a-t-il des données personnelles dans ces documents ?
Priorité 3 (SI)      : Où sont hébergées vos données aujourd'hui ?
```

## Exercice guidé

Pour ton cas, avant le rendez-vous :
1. Écris 15 questions, puis **barre les 3 moins utiles** : elles deviennent tes
   réserves.
2. Repère **la** question qui révélera le besoin réel (souvent « qu'est-ce qui
   vous fait perdre du temps ? » ou « pourquoi maintenant ? »).
3. Vérifie que **chaque question ne porte que sur un sujet** (cherche les « et »).
4. Prépare une relance type : « pouvez-vous me donner un exemple concret ? ».

*Solution attendue* : une liste de 12 questions dont les 4-5 premières couvrent
besoin, données (dont extrait), critère de succès chiffré et coût d'une erreur.

## Pièges fréquents

| Piège | Conséquence |
|---|---|
| Questions composées (« X et Y ? ») | Une seule réponse, une question gaspillée |
| Ne pas demander d'extrait de données | Qualité des données estimée à l'aveugle |
| Proposer une techno en entretien (« un LLM ferait l'affaire ? ») | On cadre une solution avant le problème |
| Garder les questions chiffrées pour la fin | Budget épuisé avant les KPI |
| Recopier la demande | On rate le besoin réel |
| Ne pas distinguer dit / interprété | Notes ambiguës, cadrage faux |

| Symptôme | Cause probable |
|---|---|
| Le client répond à côté | Question trop vague ou composée → reformuler, un sujet |
| Le client « ne comprend pas » | Jargon technique (API REST, Go…) → parler métier |
| Cadrage sans KPI chiffré | Critère de succès jamais demandé explicitement |
| On a « oublié » le RGPD | Pas de catégorie « données personnelles » préparée |
| Plus de questions à 10h20 | Pas de priorisation, questions de détail d'abord |

## Pour aller plus loin

- *Just Enough Research* (Erika Hall) : https://www.mulebooks.com/just-enough-research
- Cf. mini-cours M3-B1 (entretien) — capitalisation.

## Vérification (checklist apprenant)

- [ ] J'ai préparé 12 questions + 3 de réserve, classées par priorité.
- [ ] Chaque question ne porte que sur un sujet.
- [ ] J'ai demandé un extrait de données.
- [ ] J'ai distingué *dit* / *interprété* dans mes notes.
- [ ] J'ai posé la question imposée sur la volumétrie labellisée.
- [ ] J'ai reformulé le besoin (pas recopié la demande).

> 💡 **Récap — Entretien sous contrainte** : demande ≠ besoin ; 12 réponses → prioriser ; une question = un sujet ; ouvert sur le besoin, fermé sur les chiffres ; toujours demander un extrait ; relancer ce qui surprend ; noter dit vs interprété.
