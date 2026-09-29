# Document de cadrage — _ton cas_ (À COMPLÉTER — 3 pages max)

> **Livrable principal.** Lisible par le persona client (pas un dev). Renomme en
> `document_cadrage.md`. Les analyses (besoin, données, risques, KPI) se font
> **directement ici** : pas de fichiers séparés. Le schéma vit dans
> `schema_archi_cible.md`, tes notes dans `notes_entretien.md`.
> **3 pages est un plafond** : phrases courtes, tableaux, pas de remplissage.

## 1. Synthèse exécutive (5-6 lignes — rédigée EN DERNIER)

_Besoin réel + solution proposée (famille, pas la stack) + 2-3 indicateurs clés._

**Besoin** : Le tri des objets des mails RH mobiliserait aujourd’hui 1 h par jour pour deux personnes, soit environ 25 % d’un ETP selon l’estimation fournie.
Un classifieur supervisé pourrait orienter ces objets vers les six équipes et envoyer les cas incertains en revue humaine.
Le pilote viserait au moins 85 % de bons aiguillages et limiterait la revue manuelle à 20 % des mails au plus.
Ramener le temps total de tri, revue comprise, à 15 min par jour pour deux personnes ferait passer la charge à 6,25 % d’un ETP.
Les 2x45 min libérées chaque jour pourraient être réallouées au traitement des dossiers RH ; ces cibles resteraient à confirmer sur un échantillon représentatif.

**Solution proposées** : un classifieur supervisé de texte de la famille des modèles linéaires, par exemple une régression logistique appliquée à une représentation TF-IDF des objets des mails. Cette famille convient à une première évaluation sur les 10 000 tickets déjà classés ; un seuil de confiance pourrait envoyer les prédictions incertaines en revue.

> **Imprévu client (14h30) — ce que ça change** :

Le DPO limite l’analyse à l’objet des mails issus du ticketing.

Hypothèse : les objets ne sont pas du texte libre, mais sont issue d'un pré-formattage par l'outil de ticketting et ne contiennent pas de données sensibles. A confirmer avec le client.

Sections mises à jour : §3 à §6 et schéma.

## 2. Besoin métier et contexte (1 paragraphe)

Le tri manuel des mails RH mobilise, selon l’estimation fournie, 1 h par jour pour deux personnes, soit 25 % d’un ETP. Si le temps total de tri, revue comprise, diminue à 15 min par jour, la charge serait ramenée à 6,25 % d’un ETP : 45 min  x 2 personnes par jour pourraient être réallouées au traitement des dossiers. Le budget estimé est de 20 à 30 k€. Le système viserait au moins 85 % de bons aiguillages, avec au plus 20 % des mails envoyés en revue manuelle, basé uniquement sur l'objet du mail. Les erreurs de routage vers la paie sont particulièrement critiques en fin de mois.

## 3. Données — mini-cours `02`

| Donnée | Existante / à acquérir | Volume, qualité estimée | Personnelle ? |
| --- | --- | --- | --- |
| 10 000 tickets catégorisés | existante | bonne | Catégorie cible connue |
| Objets des tickets | Export à confirmer | Format et qualité à vérifier | Données personnelles absentes |
| Corps et pièces jointes | Présents dans les tickets | Exclus de l’analyse v1 | Données personnelles présentes |
| Échantillon (20 lignes CSV) | existant | Insuffisant mais contient les objets | Catégorie cible connue |

## 4. Risques et conformité — mini-cours `04` et `07`

**Usage réel** : le système classe l’objet du mail dans six catégories, puis le route vers l’équipe concernée. Il ne décide pas pour une personne. L’équipe peut le reclasser ; jusqu’à 20 % de revue manuelle est accepté. Corps et pièces jointes exclus.

**AI Act** : si une IA est retenue, le routage seul relève a priori du **risque minimal** (hors annexe III, point 4 : recrutement, sélection, promotion, rupture). Réévaluer toute évolution qui évalue une personne ou déclenche une action RH. Informer les agents.

**RGPD** : intérêt légitime (art. 6.1.f) à valider. Le système classe des messages, pas des personnes : pas de profilage (art. 4(4)). L’article 22 ne s’applique a priori pas au routage sans effet juridique ou significatif. Mettre à jour le registre, la notice RH et la durée de conservation. Sous-traitance externe à confirmer.

| Risque (éthique, métier, conformité) | 🔴/🟠/🟡/🟢 | Obligation ou raison | Traitement dans l'archi |
| --- | --- | --- | --- |
| Erreur de routage « paie » en fin de mois | 🔴 | Retard de salaire ou erreur de bulletin | Seuil renforcé ; sinon revue manuelle |
| Données personnelles dans le contenu des mails et pièces jointes (NIR, RIB, santé) | 🔴 | RGPD, art. 5.1.f et 9 | Risque écarté en traitant uniquement l'objet des mails. |
| Données personnelles dans les objets | 🟢 | RGPD, art. 5.1.f et 9 | Analyser l’objet seul (valider avec le clietn qu'il ne contient pas de Données personnelles) |
| Catégorie « autres » trop utilisée | 🟠 | Risque de mails non traités | Suivi du volume, alerte sur seuil et revue par un référent |
| Évolution des catégories ou motifs | 🟡 | Maintenir la performance | Suivi mensuel des reclassements ; réentraînement du modèle si seuil dépassé |
| Traçabilité insuffisante d’un mail mal aiguillé | 🟡 | Redevabilité | Journal horodaté : catégorie, destination et reclassement éventuel |

**Sécurité** — système interne, non exposé à Internet, les mails proviennent de l'outil de ticketting.

| Menace | Plausibilité sur CE cas | Mitigation proposée | Risque résiduel |
| --- | --- | --- | --- |
| Manipulation du classement via l’objet | Possible : l’expéditeur le choisit | Valider format et valeurs ; filtre anti-spam ; revue si doute | À évaluer au pilote |
| Injection de consignes | Écartée si les objet sont préformatté par l'outil de ticketting (à confirmer) | A confirmer
| Fuite de données via le système | Dépend de l’hébergement (§6) | Objet seul ; pas d’API tierce ni d’objet brut dans les logs | À confirmer |
| Empoisonnement des données d’entraînement | Écarté en v1 : jeu interne figé, sans apprentissage continu | — | — |
| Vol ou extraction du modèle | Écarté : modèle interne, sans interface exposée | — | — |
| Inférence d’appartenance | Écartée : pas d’accès externe ; sortie limitée à une catégorie | — | — |

## 5. Architecture cible et sobriété — mini-cours `05`

Le schéma montre l’extraction de l’objet depuis le ticketing, son classement, puis le routage ou la revue manuelle. Corps et pièces jointes exclus. Le suivi repose sur des journaux sans objet brut ; seuil renforcé pour _paie_.

**Choix à confirmer** : un outil entraîné à partir de tickets déjà classés (classifieur supervisé) sur les 10 000 tickets sur les objets préformattés ; un seuil de confiance pourrait envoyer les prédictions incertaines en revue. Pas de LLM en v1 : inutile et plus exposé aux injections.

Pas de modèle génératif, de recherche documentaire, ni de service externe : inutiles pour le routage. Les pièces jointes sont exclues de la v1, à confirmer avec le client.

## 6. Indicateurs, seuils, questions ouvertes — mini-cours `03`

| Indicateur métier | Départ → cible | Seuil d’acceptabilité | Mesure |
| --- | --- | --- | --- |
| Temps quotidien de tri | 1 h → 10 min | ≤ 15 min _(à valider)_ | Temps relevé, revue incluse |
| Mails envoyés à la bonne équipe | À mesurer → > 85 % | ≥ 85 % | Exactitude : Vérification RH d’un échantillon représentatif |
| Mails triés manuellement | À mesurer → < 20 % | ≤ 20 % | Précision : Mails en revue / mails reçus |
| Mails _paie_ mal triés | À mesurer → > 90% | ≥ 90 % | Rappel : Parmi les objets relevant réellement de la _paie_, part correctement détectée par le modèle |

Ces seuils sont des propositions à valider avec les RH sur un échantillon représentatif des objets des mails. Si les cibles de précision et de revue manuelle ne peuvent pas être atteintes simultanément, la sécurité du routage, notamment pour _paie_, primerait sur le taux d’automatisation.

**Prochaines étapes**

1. Vérifier le format des objets et la répartition des 10 000 tickets, surtout _matériel_ et _autres_.
2. Définir avec les RH l’échantillon de référence et les seuils, notamment pour _paie_.
3. Confirmer les périmètres technique et réglementaire avant le pilote.

**Questions ouvertes au client**

- Quel outil de ticketing est utilisé et dans quels formats les données sont-elles exportables ?
- Où la solution peut-elle être hébergée : sur site, cloud souverain ou SaaS ?
- La boîte reçoit-elle des mails externes en plus de ceux des salariés ?
- L’objet seul suffit-il au routage ? Les valeurs sont-elles standardisées ou en texte libre ?
- Qui utilisera l’outil et validera les reclassements ?
- Quel est le délai prévu et quelles solutions ont déjà été testées ?
- L’heure de tri est-elle cumulée ou par personne ?
