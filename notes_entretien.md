# Notes d'entretien — _ton cas_ (À COMPLÉTER)

> Mini-cours `01`. Ce fichier sert d'abord à **toi** ; il est aussi lu pour
> évaluer ta préparation. Renomme en `notes_entretien.md`.

## 1. Avant le rendez-vous — 12 questions + 3 de réserve

> Le client accorde **12 réponses**. **Une question à la fois**. Classe par
> priorité : si tu n'en poses que 8, ce doivent être les 8 plus utiles.
> Catégories à couvrir : besoin · processus actuel · données (existence, volume,
> qualité, **extrait**) · données personnelles / confidentialité · critère de
> succès chiffré · coût d'une erreur · utilisateurs · SI / hébergement · budget / délai.

le client : ESN ~500 salariés, Lille. Brigitte Lefranc, DRH, reçoit.
« Notre boîte mail RH reçoit 80 tickets/jour : congés, paie, mutuelle, formation, autres. On les trie à la main, ça prend 1h le matin à 2 personnes. On voudrait automatiser le tri vers les bonnes équipes. »

| # | Priorité (1-3) | Catégorie | Question |
| --- | --- | --- | --- |
| 1 | 2 | | Quelle est la répartition des types de tickets par équipe ? |
| 2 | 2 | | Quels sont les traitements par type de ticket qui sont automatisables ? |
| 3 | 1 | | Si un ticket est envoyé dans la mauvaise equipe, quel est le cout estimé pour le renvoyer vers la bonne equipe ? |
| 4 | 1 | | Quel est le cout d'un traitement manuel par type de ticket ? |
| 5 | 1 | | Quels sont vos critères de succes pour évaluer ce projet ? |
| 6 | 1 | | Quel est votre volume d'échantillons par type de tickets disponibles ? |
| 7 | 2 | | Quelles sont les données sensibles par type de ticket ? |
| 8 | 2 | | Quelles sont vos contraintes (performance, cout, reglementaire,...) ? |
| 9 | 3 | | Quels sont les formats par type de ticket ? |
| 10 | 3 | | Quelle est la qualité du format par type de ticket ? |
| 11 | 2 | | Quelle est la part d'automatisation que vous souhaitez mettre en place : seulement le tri ou une partie des traitements aussi ? |
| 12 | 3 | | Quelle est la proportion de ticket qui arrivent en "autre" ? |
| R1 | réserve | 3 | Quel est le jeu de données disponible ? |
| R2 | réserve | 3 | Quelles sont les données ? |
| R3 | réserve | | |

## 2. Pendant le rendez-vous — dit / interprété

| Question posée (telle quelle) | Ce que le client a **dit** (citation) | Ce que j'en **interprète** |
|---|---|---|
|Quelle est la répartition des types de tickets par équipe ? | Historiquement cinq : congés, paie, mutuelle, formation et « autre ». Depuis l'an dernier on a ajouté « matériel », parce qu'on reçoit plein de demandes d'écran ou de PC qui devraient aller à la DSI. Donc pour matériel on a peu d'historique, et avant on les rangeait dans « autre ». | Traitement supervisé de mail (donnée textuelles) en 6 categories, classe déséquilibrée (surtout materiel) |
|Quels sont les traitements par type de ticket qui sont automatisables ? | Tous les matins, deux personnes de mon équipe passent environ une heure à lire la boîte rh@ et à transférer chaque mail à la bonne équipe : congés, paie, mutuelle, formation… C'est une heure où elles ne traitent aucun dossier. Et quand quelqu'un est absent, les tickets s'accumulent et les salariés relancent. | Uniquement le tri, pas le traitement. Objectif secondaire : fluidifier pour réduire les relances. Cout estimé : 2h/j, soit ~2j/sem, soit~8j/mois|
|Si un ticket est envoyé dans la mauvaise equipe, quel est le cout estimé pour le renvoyer vers la bonne equipe ? |Ce n'est pas dramatique : l'équipe qui le reçoit le renvoie à la bonne. On perd un jour ou deux. Sauf pour la paie juste avant la clôture du mois, là une erreur peut faire rater une régularisation, et ça le salarié ne le pardonne pas.|Accuracy plus importante que le recall, sauf sur la paie|
|Quel est le cout d'un traitement manuel par type de ticket ? |Oui, très bien, si l'outil dit « je ne sais pas » sur une partie des tickets et qu'on les trie nous-mêmes, ça me va. Tant que c'est une petite partie, disons moins d'un ticket sur cinq.| Cible : max 20% des tickets peuvent etre triés manuellement|
|Quels sont vos critères de succes pour évaluer ce projet ? |Si on passe d'une heure de tri par jour à dix minutes, c'est gagné. Et il faut que ce soit juste : je dirais que plus de 85 % des tickets doivent arriver directement dans la bonne équipe.| Cible : min 85% d'accuracy|
|Quel est votre volume d'échantillons par type de tickets disponibles ? |Environ 80 tickets par jour en moyenne. Avec des pics : en janvier pour la mutuelle, en mai-juin pour les congés, et à chaque fin de mois pour la paie, là on peut monter à 150. |Série temporelle probable car périodicité|
|Quelles sont les données sensibles par type de ticket ? |Ah oui, il faut faire très attention. Les gens mettent leur numéro de sécurité sociale, leur salaire, et pour la mutuelle, parfois des informations de santé : un arrêt, une hospitalisation. Je ne veux pas que ces données partent n'importe où.|Données sensibles (RGPD), contrainte de stockage souverain forte|
|Quelles sont vos contraintes (performance, cout, reglementaire,...) ? |On n'a pas un budget énorme. Mon directeur a parlé de 20 à 30 000 euros pour la première année, maintenance comprise. Il faut que ça se rentabilise : deux personnes une heure par jour, faites le calcul.| Budget client : 20 à 30K€|
|Quels sont les formats par type de ticket ? |Un objet, un corps de mail, souvent court, et parfois des pièces jointes : des arrêts de travail, des factures d'opticien, des bulletins de paie. Les mails sont en français, quelques-uns en anglais pour nos consultants étrangers.| Type de donnée : textuelle, avec pièce jointe, langue français et anglais. |
| Quelle est la qualité du format par type de ticket ? |Globalement fiables, mais pas parfaites. Mes deux assistantes n'ont pas toujours la même logique : une question « arrêt maladie et salaire », l'une la met en paie, l'autre en autre. Et quand on est pressées, « autre » sert un peu de fourre-tout.| Critères de tri manuels non harmonisés. |
| Quelle est la part d'automatisation que vous souhaitez mettre en place : seulement le tri ou une partie des traitements aussi ? |Tous les matins, deux personnes de mon équipe passent environ une heure à lire la boîte rh@ et à transférer chaque mail à la bonne équipe : congés, paie, mutuelle, formation… C'est une heure où elles ne traitent aucun dossier. Et quand quelqu'un est absent, les tickets s'accumulent et les salariés relancent. | Voir questions précédentes|
| Quelle est la proportion de ticket qui arrivent en "autre" ? | Le chiffre exact, je ne l'ai pas en tête. Pas mal, parce qu'on s'en sert de fourre-tout quand on est pressées, et parce que le matériel y était rangé avant l'an dernier. Tout est dans l'outil de ticketing : vous le verrez dans les données.|Proportion autre assez forte  et contenant la nouvelle categroei materielle (classes déséquilibrées)|
| Quel est le jeu de données disponible ? |On a quelques serveurs dans un datacenter à Lille, et Microsoft 365 pour la messagerie. Pour les données RH, la DPO veut que tout reste en France ou au moins en Europe, avec un contrat clair.|Contrainte de stockage souverain (France ou Europe) forte.|
| Quelles sont les données ? |Oui, notre outil de ticketing garde tout. On a à peu près 10 000 tickets depuis trois ans, et chacun a déjà sa catégorie puisque c'est nous qui l'avons choisie à la main au moment du tri.| Dataset de 10K avec target|

_Relance non prévue ? Note-la aussi, avec la raison (« réponse surprenante sur… »)._

### Boussole — ce que j'ai déjà obtenu

> Mets-la à jour **après chaque réponse**. Elle suit des **informations**, pas
> tes questions : une réponse peut en remplir plusieurs, une autre aucune.
> Quand il te reste 3-4 questions, regarde les 🔴 : lequel manquera le plus à
> ton cadrage ? C'est à toi de formuler la question.
>
> 🟢 obtenu · 🟠 partiel / à vérifier · 🔴 à obtenir · ⬜ pas demandé (→ §3)

| Information | Statut | Réponse n° |
| --- | --- | --- |
| Besoin réel (≠ demande exprimée) | 🟢 | |
| Processus actuel | 🟠 | |
| Données : existence | 🟢 | |
| Données : volume | 🟢 | |
| Données : qualité | 🟠 | |
| Données : extrait obtenu | 🟢 | |
| Données personnelles / confidentialité | 🟢 | |
| Critère de succès chiffré | 🟢 | |
| Coût d'une erreur | 🟢 | |
| Erreurs tolérées (chiffre : fausses alertes, mauvais routage…) | 🟢 | |
| Utilisateurs | 🔴 | |
| Validation humaine / qui décide | 🔴 | |
| SI / hébergement | 🟢 | |
| Budget | 🟢 | |
| Délai | 🟠 | |
| Ce qui a déjà été essayé | 🔴 | |

## 3. Après — ce que je n'ai pas pu demander → questions ouvertes

| Je n'ai pas pu demander / pas eu de réponse claire | Pourquoi c'est important | → §6 du cadrage |
| --- | --- | --- |
| Mieux cerner l'outil de ticketing existant | Permet de comprendre ce qui est saisi et dans quel format | |
| **Hébergement** : où la solution peut-elle tourner ? On-premise, cloud souverain, ou SaaS autorisé ? | impacte directement le traitement des PII et l'éligibilité d'un LLM externe | |
| **Périmètre des expéditeurs** : la boîte RH reçoit-elle uniquement des mails de salariés internes, ou aussi de candidats, prestataires et organismes externes ? | impacte le volume, la qualité et le risque d'entrée non maîtrisée | |
| **Pièces jointes** : doivent-elles être analysées pour décider du routage, ou le corps du mail suffit-il ? | Impacte les données d'entrée à analyser | |
