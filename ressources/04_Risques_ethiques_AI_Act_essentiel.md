# Risques éthiques + qualification AI Act — Mini-cours

> Brief associé : M8-B1
> Durée de lecture : ~25 min
> Pré-requis : RGPD/AI Act vus en M7-B1 (qualifier par l'usage, pas par le secteur)

## Pourquoi cette techno ?

Identifier les risques **dès le cadrage** (pas en audit a posteriori) évite de
concevoir un projet non conforme : un risque repéré tôt se traite dans
l'architecture. Mais un risque mal **qualifié** coûte aussi : présumer « haut
risque » impose des obligations lourdes injustifiées ; l'écarter trop vite
expose le client. Le geste attendu n'est pas une **étiquette** posée en 2
minutes, c'est une **qualification documentée** : l'usage réel, le cas du
texte qui s'applique (ou pas), et ce qui ferait basculer. C'est ce raisonnement
— pas le mot « limité » ou « élevé » — que regarde un DPO, et un jury.

## Concepts clés

- **Les niveaux de l'AI Act, correctement** :
  - *pratiques interdites* (art. 5 : notation sociale, manipulation…) ;
  - *haut risque* (art. 6) : **produit réglementé** dont l'IA est un composant de
    sécurité (Annexe I : dispositifs médicaux, machines…) **ou** **cas d'usage
    listé** en Annexe III (ex. recrutement et gestion des travailleurs, accès
    aux services essentiels, triage des urgences, IA utilisée **par une autorité
    judiciaire**…), sauf exception 6(3) — fermée en cas de profilage ;
  - *obligations de transparence* (art. 50) : système qui **interagit** avec des
    personnes (chatbot), contenus générés ou manipulés ;
  - *le reste* : pas d'obligation spécifique (bonnes pratiques, maîtrise de
    l'IA par les équipes, art. 4). **C'est le cas de la plupart des outils
    internes.**
- **On qualifie un usage, pas un secteur** : « RH » n'est pas haut risque en
  soi — **trier des candidatures** l'est (Annexe III, 4 a) ; router des tickets
  vers le bon service ne l'est pas, **sauf** si l'outil sert à évaluer les
  agents. Même logique en santé, justice, industrie.
- **RGPD, s'applique toujours** (dès qu'il y a des données personnelles) :
  **base légale à déterminer et justifier** (art. 6 : contrat, intérêt légitime,
  consentement… — aucune n'est acquise d'office), minimisation, information des
  personnes, **profilage** à identifier. L'**art. 22** ne vise qu'une décision
  **exclusivement automatisée** produisant un effet **juridique ou similairement
  significatif**. Art. 9 si données sensibles (santé, mutuelle).
- **Risques métier** : secret professionnel, surveillance des salariés, sécurité
  industrielle, bulle de filtre… — ceux que le texte ne liste pas mais que le
  client paiera.
- **Sévérité + traitement dans l'architecture** : chaque risque 🔴/🟠/🟡, son
  obligation ou sa raison, et **où** l'archi le traite (pseudonymisation, revue
  humaine, journalisation).

## Exemple minimal qui tourne

Deux usages RH d'un même client — **pas les cas du brief** :

```markdown
Usage 1 — pré-tri automatique des CV reçus
- Usage réel : score qui écarte ~60 % des candidatures avant lecture humaine.
- AI Act : Annexe III 4 a (recrutement, filtrage des candidatures) → HAUT RISQUE.
  6(3) ? non : profilage + influence directe.
- RGPD : art. 22 plausible (candidats écartés sans examen humain) → à instruire.

Usage 2 — FAQ interne qui répond aux salariés sur les congés
- Usage réel : chatbot, réponses citant l'accord d'entreprise, pas de décision.
- AI Act : pas de cas Annexe III → pas haut risque ; art. 50 : dire aux salariés
  qu'ils parlent à une IA. Bascule si : l'outil accorde/refuse des congés.
- RGPD : questions contenant des données perso → base légale + conservation.
```

## Exercice guidé

Pour ton cas, dans la section risques de ton document de cadrage :
1. Écris l'**usage réel** en 3 lignes : qui utilise la sortie, qu'est-ce qu'elle
   déclenche, un humain peut-il la contredire ?
2. **Qualifie** (interdit / haut risque / transparence / sans obligation
   spécifique) en citant le cas du texte — ou pourquoi aucun ne s'applique —
   et la **condition de bascule**.
3. RGPD : **quelle base légale** proposes-tu, pourquoi celle-là, et y a-t-il du
   profilage ? L'art. 22 s'applique-t-il (2 conditions) ?
4. Liste 5-7 risques 🔴/🟠/🟡 ; pour chaque 🔴, un traitement **dans l'archi**.

## Pièges fréquents

| Piège | Conséquence |
|---|---|
| Qualifier par le secteur (« santé / justice / RH = haut risque ») | Étiquette fausse, obligations plaquées |
| « Outil interne = risque limité » | Confond avec les obligations de transparence (art. 50) |
| Base légale posée d'office (« exécution du contrat ») | Non justifiée, contestable par le DPO |
| « Art. 22 » dès qu'il y a une prédiction | Oublie les 2 conditions cumulatives |
| Risque sans traitement dans l'archi | Non actionnable |

| Symptôme | Cause probable |
|---|---|
| Le DPO conteste la qualification | usage réel non décrit, cas du texte non cité |
| Toutes les obligations « haut risque » listées pour un outil interne | présomption au lieu de qualification |
| PII oubliées | pas de revue RGPD au cadrage |
| Risques tous au même niveau | pas de sévérité différenciée |

## Pour aller plus loin

- AI Act — texte consolidé EUR-Lex (art. 5, 6, 50, Annexe III) : https://eur-lex.europa.eu/eli/reg/2024/1689/oj
- RGPD — EUR-Lex (art. 6, 21, 22) : https://eur-lex.europa.eu/legal-content/FR/TXT/?uri=CELEX%3A32016R0679
- CNIL — IA et RGPD : https://www.cnil.fr/fr/intelligence-artificielle/ia-comment-etre-en-conformite-avec-le-rgpd

## Vérification (checklist apprenant)

- [ ] J'ai décrit l'**usage réel** avant de qualifier.
- [ ] Ma qualification AI Act cite le cas du texte (ou pourquoi aucun) + la condition de bascule.
- [ ] J'ai **proposé et justifié** une base légale RGPD, identifié le profilage éventuel.
- [ ] 5-7 risques 🔴/🟠/🟡, les 🔴 traités dans l'architecture.
- [ ] Les risques métier du secteur sont identifiés.

> 💡 **Récap — Risques + AI Act** : **décrire l'usage**, puis **qualifier** (interdit / haut risque art. 6 + Annexe I ou III / transparence art. 50 / sans obligation spécifique) **avec le raisonnement et la condition de bascule**. RGPD : base légale **à justifier**, profilage, art. 22 seulement si décision exclusivement automatisée à effet significatif. Les 🔴 se traitent **dans l'architecture**.

### À retenir

- Le livrable se juge sur sa **clarté pour le destinataire**, pas sur sa longueur.
- **Chiffrer** plutôt qu'affirmer : un nombre vaut mieux qu'un adjectif.
- **Sobriété** : recommander le plus simple qui résout le besoin, et **dire ce qu'on écarte**.
- Distinguer ce qu'on **sait** de ce qui reste **à clarifier** (questions ouvertes).
- Tracer ses **choix** et leur **raison** — c'est ce qui se défend en restitution.
