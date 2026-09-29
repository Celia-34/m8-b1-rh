# M8-B1 — Cadrer un projet IA en autonomie chez un client (3 cas)

> **Repo template.** « Use this template » → `M8-B1-cadrage-<prenom>`. La
> formatrice t'affecte un client (cas A, C ou D). Tu mènes un **rendez-vous en
> ligne** avec ce client fictif, puis tu rédiges un cadrage de **3 pages**.
> **Pas de code** : posture consultant. Individuel, **mardi 9h15-15h30**, aucun
> asynchrone.

## 🗓️ Ta journée

| Heure | À faire | Fichier | Mini-cours |
|---|---|---|---|
| 9h15-10h00 | Lire le briefing de ton cas (MP Discord), créer ton repo, **préparer 12 questions** (+ 3 de réserve) classées par priorité | `notes_entretien.md` | `01` |
| 10h00-10h45 | **Rendez-vous client en ligne** (URL sur Discord + ton code perso en MP). **12 réponses max**, **une question à la fois**. Un fichier envoyé par le client apparaît dans « Documents transmis » : télécharge-le dans ton repo | `notes_entretien.md` | `01` |
| 10h45-12h30 | Cadrage **§2 besoin, §3 données, §4 risques & conformité** | `document_cadrage.md` | `02`, `04`, `07` |
| 13h30-14h30 | **§5 architecture** (Mermaid) + sobriété, **§6 KPI** + questions ouvertes | `schema_archi_cible.md`, `document_cadrage.md` | `05`, `03` |
| 14h30 | **Imprévu client** posté sur Discord : identifier ce qu'il change, mettre à jour les sections concernées | `document_cadrage.md` | — |
| 14h30-15h30 | **§1 synthèse** (en dernier), relecture « persona client » | `document_cadrage.md` | `06` |
| **15h30** | **Commit « cadrage final » poussé.** Ensuite, bascule en **M8-B2** avec les collègues du même client | — | — |

> Renomme les `*_TEMPLATE.md` en `notes_entretien.md`, `schema_archi_cible.md`,
> `document_cadrage.md`. Le rendez-vous est **journalisé** : la qualité de tes
> questions compte dans l'évaluation.

## 🏢 Les 3 clients

- **A — Cabinet Maître Devalle** (juridique, 12 avocats) : courriers types + recherche de jurisprudence.
- **C — CapGroup Services** (ESN, DRH) : tri automatique de ~80 tickets RH/jour.
- **D — Galvaplus Industries** (galvanisation) : être prévenu 48 h avant une panne de bain.

Le briefing complet de **ton** cas t'est envoyé en MP.

## ✅ Réussite

- **12 questions préparées et priorisées**, relances pertinentes pendant le rendez-vous.
- Besoin **reformulé** (≠ recopié). Données existantes vs à acquérir, qualité estimée.
- Risques 🔴/🟠/🟡 + traitement dans l'archi. **Qualification AI Act et base
  légale RGPD raisonnées** (usage réel décrit). ≥ 2 menaces de sécurité + mitigation.
- Archi Mermaid ≥ 4 composants. **Sobriété argumentée** (LLM retenu/refusé : 3 lignes).
- KPI **chiffrés** + seuils. **Imprévu client intégré**.
- **3 pages max**, lisible **par le client**. ≥ 3 commits. **Journal de bord** tenu.

## 📚 Ressources

Voir [`./ressources/`](./ressources/) — 7 mini-cours (dont sécurité modèle) + `liens_officiels.md`.
