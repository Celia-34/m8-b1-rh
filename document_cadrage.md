# Document de cadrage — _ton cas_ (À COMPLÉTER — 3 pages max)

> **Livrable principal.** Lisible par le persona client (pas un dev). Renomme en
> `document_cadrage.md`. Les analyses (besoin, données, risques, KPI) se font
> **directement ici** : pas de fichiers séparés. Le schéma vit dans
> `schema_archi_cible.md`, tes notes dans `notes_entretien.md`.
> **3 pages est un plafond** : phrases courtes, tableaux, pas de remplissage.

## 1. Synthèse exécutive (5-6 lignes — rédigée EN DERNIER)

_Besoin réel + solution proposée (famille, pas la stack) + 2-3 indicateurs clés._

> **Imprévu client (14h30) — ce que ça change** : _1-2 lignes : quelle contrainte
> a bougé, quelles sections tu as mises à jour (données ? risques ? archi ? KPI ?)._

## 2. Besoin métier et contexte (1 paragraphe)

_Demande exprimée (citation) vs **besoin réel reformulé**. Contraintes révélées
en entretien (budget, équipe, confidentialité…)._

Le tri manuel des mails RH vers les équipes prend environ 1 h/jour et représente 25 % d’un ETP. L’automatiser permettrait de consacrer plus de temps aux dossiers. Budget : 20 à 30 k€. Objectif : automatiser au moins 85 % du tri, avec au plus 20 % de revue manuelle. Les erreurs de routage vers la paie sont particulièrement critiques en fin de mois.

## 3. Données — mini-cours `02`

| Donnée | Existante / à acquérir | Volume, qualité estimée | Personnelle ? |
| --- | --- | --- | --- |
| 10k tickets catégorisés | existante | bonne | dataset labellisé (target) |
| Texte des tickets | existante | variable | PII présentes |
| Pièce jointe des tickets | ? | variable | PII présentes |
| Échantillon (20 lignes CSV) | existant | insuffisant | non |

## 4. Risques et conformité — mini-cours `04` et `07`

**Usage réel** : le modèle classe chaque mail dans l’une des six catégories (congés, paie, mutuelle, formation, matériel, autres), puis l’envoie à l’équipe concernée. Il oriente un message, sans décider pour une personne. L’équipe peut le reclasser ; jusqu’à 20 % de revue manuelle est accepté.

**Qualification AI Act** : **risque minimal** pour ce simple routage, hors recrutement, sélection, promotion ou rupture de contrat (annexe III, point 4). Si une évolution évalue des personnes ou déclenche une action RH, les exigences de l’annexe III (documentation, gestion des risques, supervision) devront être réévaluées. Les agents seront informés du tri automatique.

**RGPD** : l’intérêt légitime (art. 6.1.f) peut justifier l’organisation du tri, sous réserve de validation. Le système classe des messages, pas des personnes : pas de profilage (art. 4(4)). L’article 22 ne s’applique pas au routage seul, sans décision produisant d’effet juridique ou significatif. À prévoir : registre des traitements à jour, information dans la notice RH et conservation alignée sur celle des tickets. Aucun sous-traitant externe n’est prévu, c'est à confirmer avec le client.

| Risque (éthique, métier, conformité) | 🔴/🟠/🟡 | Obligation ou raison | Traitement dans l'archi |
| --- | --- | --- | --- |
| Erreur de routage « paie » en fin de mois | 🔴 | Retard de salaire ou erreur de bulletin | Seuil renforcé ; sinon revue manuelle |
| PII dans les mails et pièces jointes (NIR, RIB, santé) | 🔴 | RGPD, art. 5.1.f et 9 | Infrastructure maîtrisée ; pas d’API publique ; texte non conservé après routage ; logs pseudonymisés |
| Catégorie « autres » trop utilisée | 🟠 | Risque de mails non traités | Suivi du volume, alerte sur seuil et revue par un référent |
| Évolution des catégories ou motifs | 🟡 | Maintenir la performance | Suivi mensuel des reclassements ; réentraînement si seuil dépassé |
| Traçabilité insuffisante d’un mail mal aiguillé | 🟡 | Redevabilité | Journal horodaté : catégorie, destination et reclassement éventuel |

**Sécurité du modèle** — système interne, non exposé à Internet, mais recevant des mails d’expéditeurs variés par l'outil de ticketting. L’entrée est le principal vecteur de risque.

| Menace | Plausibilité sur CE cas | Mitigation proposée | Risque résiduel |
| --- | --- | --- | --- |
| Manipulation du classement par l’expéditeur | Élevée : boîte ouverte aux messages entrants | Filtre anti-spam ; suivi des expéditeurs souvent reclassés | Faible : correction manuelle, sans fuite |
| Injection de consignes dans le mail | Nulle avec le classifieur classique ; à réévaluer si un LLM est retenu | Pas de LLM en v1 ; sortie limitée aux six catégories | Faible en v1 |
| Fuite de données via le modèle | Dépend de l’hébergement, à confirmer (§6) | Hébergement maîtrisé ; pas d’API tierce ni de réutilisation sans anonymisation | Faible |
| Empoisonnement des données d’entraînement | Écarté en v1 : jeu interne figé, sans apprentissage continu | — | — |
| Vol ou extraction du modèle | Écarté : modèle interne, sans interface exposée | — | — |
| Inférence d’appartenance | Écartée : pas d’accès externe ; sortie limitée à une catégorie | — | — |

## 5. Architecture cible et sobriété — mini-cours `05`

Le schéma de `schema_archi_cible.md` montre le flux : boîte RH, préparation, classification, contrôle de confiance, puis routage ou revue manuelle. Les journaux pseudonymisés alimentent le suivi des performances. Le seuil sera renforcé pour _paie_.

**LLM non retenu en v1** : un classifieur supervisé suffit pour six catégories et 10 000 tickets labellisés. Il réduit aussi le risque d’injection de consignes. Un LLM pourra être réévalué si les résultats sont insuffisants.

Pas de RAG, de base vectorielle ni d’API externe : inutiles pour le routage. Les pièces jointes sont exclues de la v1, à confirmer avec le client.

## 6. Indicateurs, seuils, questions ouvertes — mini-cours `03`

| Indicateur métier | Départ → cible | Seuil d’acceptabilité | Mesure |
| --- | --- | --- | --- |
| Temps quotidien de tri | 1 h → 10 min | ≤ 15 min _(à valider)_ | Temps relevé, revue incluse |
| Mails envoyés à la bonne équipe | À mesurer → > 85 % | ≥ 85 % | Vérification RH d’un échantillon représentatif |
| Mails triés manuellement | À mesurer → < 20 % | ≤ 20 % | Mails en revue / mails reçus |

L’exactitude globale et les résultats pour _paie_ seront suivis. Vu le coût d’une erreur en fin de mois, les mails _paie_ sous le seuil renforcé seront revus manuellement. Ce seuil reste à définir.

**Prochaines étapes**

1. Vérifier la qualité et la répartition des 10 000 tickets, surtout _matériel_ et _autres_.
2. Définir avec les RH l’échantillon de référence et les seuils, notamment pour _paie_.
3. Confirmer les périmètres technique et réglementaire avant le pilote.

**Questions ouvertes au client**

- Quel outil de ticketing est utilisé et dans quels formats les données sont-elles exportables ?
- Où la solution peut-elle être hébergée : sur site, cloud souverain ou SaaS ?
- La boîte reçoit-elle des mails externes en plus de ceux des salariés ?
- Le corps suffit-il au routage ou faut-il analyser les pièces jointes ?
- Qui utilisera l’outil et validera les reclassements ?
- Quel est le délai prévu et quelles solutions ont déjà été testées ?
- L’heure de tri est-elle cumulée ou par personne ?
