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

## 3. Données — mini-cours `02`
| Donnée | Existante / à acquérir | Volume, qualité estimée | Personnelle ? |
|---|---|---|---|
| | | | |

_Si le client t'a transmis un extrait : 1-2 constats de qualité observés dessus.
Ce que tu n'as pas demandé n'existe pas : écris-le en question ouverte (§6)._

## 4. Risques et conformité — mini-cours `04` et `07`

**Usage réel** (2-3 lignes) : _qui utilise la sortie, ce qu'elle déclenche, qui peut la contredire._

**Qualification AI Act** : _niveau + cas du texte (ou pourquoi aucun) + condition de bascule._

**RGPD** : _base légale proposée et pourquoi ; profilage ? art. 22 (2 conditions) ?_

| Risque (éthique, métier, conformité) | 🔴/🟠/🟡 | Obligation ou raison | Traitement dans l'archi |
|---|---|---|---|
| | | | |

**Sécurité du modèle** — selon l'**exposition** de ton archi : 2 menaces
plausibles minimum, les autres écartées en 1 ligne. Mitiger ≠ supprimer.

| Menace | Plausibilité sur CE cas | Mitigation proposée | Risque résiduel |
|---|---|---|---|
| | | | |

## 5. Architecture cible et sobriété — mini-cours `05`
_Renvoi à `schema_archi_cible.md` (Mermaid ≥ 4 composants). **LLM retenu ou
refusé : 3 lignes.** Ce que tu écartes, et pourquoi._

## 6. Indicateurs, seuils, questions ouvertes — mini-cours `03`
| Indicateur | Cible | Seuil d'acceptabilité | Comment on le mesure |
|---|---|---|---|
| | | | |

_Prochaines étapes (3) + **questions ouvertes** au client (reprises de `notes_entretien.md` §3)._
