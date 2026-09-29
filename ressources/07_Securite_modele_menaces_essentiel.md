# Sécurité d'un système IA — menaces et robustesse — Mini-cours

> Brief associé : M8-B1
> Durée de lecture : ~25 min
> Pré-requis : risques éthiques (mini-cours 04), 3 archis M7-B2

## Pourquoi cette techno ?

Un système IA a des **vulnérabilités propres**, en plus de celles d'une appli
classique : on peut tromper le modèle, empoisonner ses données, lui faire fuiter
ce qu'il a appris. Ces menaces se traitent **au cadrage**, comme les risques
éthiques : le niveau de menace dépend de l'**exposition** — un modèle interne en
batch ≠ une API publique ≠ un agent avec droits d'écriture. C'est donc un
**critère de conception** (quelle archi expose quoi ?), pas un sujet d'audit a
posteriori. La cartographie de référence côté attaquant est **MITRE ATLAS**
(culture — on ne l'applique pas en entier ici).

## Concepts clés

- **Surface d'attaque d'un système IA** : 4 points d'entrée — les **données
  d'entraînement** (qui les fournit ? la boucle est-elle ouverte ?), le **modèle**
  lui-même (fichier, poids), l'**API d'inférence** (qui peut l'appeler, combien de
  fois ?), et les **prompts/documents** pour un système LLM/RAG. Cartographier la
  surface = repérer lesquels de ces 4 points sont exposés dans TON archi cible.
- **Adversarial examples** : entrées **légèrement modifiées** pour tromper le
  modèle sans qu'un humain voie la différence — image de panneau STOP avec
  autocollants classée « limitation 45 », spam avec caractères substitués
  (v1agra, homoglyphes Unicode) qui passe le filtre. Pertinent dès que
  l'**attaquant contrôle l'entrée** et a intérêt à tromper.
- **Data poisoning** : empoisonnement du **jeu d'entraînement** — l'attaquant
  glisse des exemples piégés pour biaiser le futur modèle. Plausible surtout si
  la **boucle de feedback est ouverte** (le modèle réapprend sur des données que
  des utilisateurs peuvent produire — cf. boucle de réentraînement M6).
- **Prompt injection & jailbreak** (spécifique LLM/RAG/agents) : instructions
  malveillantes glissées dans l'entrée (« ignore tes consignes et... ») ou —
  plus sournois — **injection indirecte** : l'instruction est cachée dans un
  **document que le RAG indexe** et remonte au modèle. Pertinent pour les cas
  qui penchent GenAI ; sans objet pour un modèle tabulaire.
- **Extraction et fuite** : **vol de modèle** (reconstruire le modèle en
  interrogeant massivement l'API) et **fuite de données d'entraînement** (le
  modèle régurgite des exemples mémorisés — PII, clauses confidentielles).
  Pertinent si l'API est largement exposée ou si l'entraînement contient du
  sensible.

**Mitigations — l'état de l'art en une ligne chacune** :

- **Validation / assainissement des entrées** (input sanitizer) : normaliser,
  tronquer, filtrer les patterns suspects avant le modèle.
- **Moindre privilège pour les agents** : droits minimaux, jamais d'écriture
  non nécessaire.
- **Séparation instructions / données** : le contenu utilisateur ou documentaire
  n'est jamais traité comme une consigne.
- **Monitoring des anomalies d'usage** : volumes d'appels, entrées atypiques,
  taux d'erreur — brancher sur le monitoring déjà prévu (M5/M6).
- **Human-in-the-loop sur les actions sensibles** : validation humaine avant
  toute action irréversible.

Aucune mitigation n'annule la menace : on note le **risque résiduel** et on
décide s'il est acceptable — c'est ça, « évaluer les risques résiduels ».

## Exemple minimal qui tourne

Threat-model du cas D (Galvaplus — maintenance prédictive, capteurs IoT,
modèle interne, alerte 48 h) :

```markdown
| Menace | Plausibilité sur CE cas | Mitigation proposée | Risque résiduel |
|---|---|---|---|
| Poisoning via capteurs compromis | 🟠 réseau OT accessible | validation plages physiques (t°, pH) + monitoring anomalies capteurs | capteur dérivant lentement sous les seuils |
| Adversarial example sur l'entrée | 🟡 faible : pas d'attaquant qui « soumet » une entrée | — (exposition interne batch) | accepté |
| Prompt injection | ⚪ sans objet : pas de LLM dans l'archi | — | — |
| Extraction de modèle via API | 🟡 API interne, appels limités | authentification + rate limiting | insider motivé |
```

Noter le geste : **⚪ sans objet argumenté vaut mieux qu'une menace copiée-collée**
— la plausibilité dépend de l'exposition de l'archi, pas d'un catalogue.

## Exercice guidé

Pour ton cas :
1. Repère les points de ta **surface d'attaque** réellement exposés (données ?
   API ? boucle de feedback ? documents RAG ?) d'après ton `schema_archi_cible.md`.
2. Remplis le tableau menace / plausibilité / mitigation / risque résiduel de
   la section 4 de `document_cadrage.md` — **2-3 menaces plausibles**, les autres écartées en
   une ligne.
3. Vérifie la cohérence : si tu écartes le LLM dans ton archi, la prompt
   injection est **sans objet** — et inversement.

## Pièges fréquents

| Piège | Conséquence |
|---|---|
| Catalogue de menaces sans lien avec le cas | Non actionnable, cadrage hors-sol |
| Ignorer l'exposition (batch ≠ API ≠ agent) | Menaces sur- ou sous-estimées |
| Prompt injection sur un modèle tabulaire | Incohérence archi ↔ menaces |
| Mitigation sans risque résiduel | On croit la menace « réglée » |
| Oublier la boucle de feedback (poisoning) | Angle mort si réentraînement prévu (M6) |
| Traiter la sécurité en audit a posteriori | Archi à refaire après coup |

| Symptôme | Cause probable |
|---|---|
| Toutes les menaces au même niveau | plausibilité non évaluée sur CE cas |
| Menace citée pour une brique absente de l'archi | copie de catalogue, pas d'analyse |
| « Aucun risque, c'est interne » | surface d'attaque non cartographiée (insider, capteurs) |
| Mitigations toutes génériques (« sécuriser l'API ») | pas de lien mitigation ↔ menace précise |
| Risque résiduel jamais mentionné | confusion mitigation = suppression de la menace |

## Pour aller plus loin

- MITRE ATLAS (cartographie des attaques sur les systèmes IA) : https://atlas.mitre.org/
- OWASP Top 10 for LLM Applications : https://owasp.org/www-project-top-10-for-large-language-model-applications/
- ANSSI — Recommandations de sécurité pour un système d'IA générative : https://cyber.gouv.fr/publications/recommandations-de-securite-pour-un-systeme-dia-generative
- NIST AI 100-2 (taxonomie adversarial ML) : https://csrc.nist.gov/pubs/ai/100/2/e2023/final

## Vérification (checklist apprenant)

- [ ] J'ai cartographié la surface d'attaque de MON archi cible (4 points).
- [ ] J'ai identifié 2-3 menaces **plausibles** pour mon cas (et écarté les autres en 1 ligne).
- [ ] Chaque menace retenue a une mitigation **et** un risque résiduel.
- [ ] Mes menaces sont cohérentes avec mon archi (pas de prompt injection sans LLM).
- [ ] Je peux expliquer pourquoi batch interne ≠ API publique ≠ agent avec droits d'écriture.

> 💡 **Récap — Sécurité du modèle** : 4 points de surface (données, modèle, API, prompts/docs) ; 5 familles de menaces (adversarial, poisoning, injection/jailbreak, extraction, fuite) ; le niveau de menace dépend de l'**exposition** → critère de **conception**, à traiter au cadrage. Mitiger ≠ supprimer : toujours nommer le **risque résiduel**. MITRE ATLAS = cartographie de référence (culture).

### À retenir

- Le livrable se juge sur sa **clarté pour le destinataire**, pas sur sa longueur.
- **Chiffrer** plutôt qu'affirmer : un nombre vaut mieux qu'un adjectif.
- **Sobriété** : recommander le plus simple qui résout le besoin, et **dire ce qu'on écarte**.
- Distinguer ce qu'on **sait** de ce qui reste **à clarifier** (questions ouvertes).
- Tracer ses **choix** et leur **raison** — c'est ce qui se défend en restitution.
