# Document de cadrage en 3 pages — Mini-cours

> Brief associé : M8-B1
> Durée de lecture : ~20 min
> Pré-requis : entretien mené, notes prises — les analyses se rédigent **dans** le document
> *(nom de fichier historique « 5pages » : le format actuel est 3 pages)*

## Pourquoi cette techno ?

Le document de cadrage est le **livrable client** qui synthétise tout : il convertit
ton analyse en un document **décisionnel** que le client (Devalle, Lefranc,
Combaud) peut lire et **valider**. **3 pages max** : assez pour être complet,
assez court pour être lu par un décideur pressé, et rédigeable en une journée.
C'est l'exercice de synthèse qui boucle le cadrage (CT5/CT6).

## Concepts clés

- **3 pages, 6 sections, un seul fichier** : synthèse exec / besoin+contexte /
  données / risques & conformité / archi+sobriété / KPI+questions ouvertes. Pas de
  fichiers d'analyse à recopier : on écrit directement ici.
- **Densité** : tableaux plutôt que paragraphes (données, risques, KPI) ; une idée
  par phrase. Le plafond de 3 pages oblige à choisir, c'est voulu.
- **Synthèse exécutive rédigée en dernier, placée en premier** : besoin, solution
  proposée, indicateurs clés — la seule partie que lira un décideur pressé.
- **Imprévu client intégré** : quand le client change une contrainte, on met à
  jour les sections touchées **et** on le dit en une ligne dans la synthèse.
- **Lisible par le persona** : pas un seul terme technique non défini.
  « classifieur de texte » oui, `TF-IDF` à expliquer ou éviter.
- **Sobriété argumentée** : 3 lignes justifiant le choix (ou non) d'un LLM.
- **Questions ouvertes** : finir par ce qui reste à clarifier (preuve de lucidité).

## Exemple minimal qui tourne

```markdown
## 1. Synthèse exécutive
CapGroup trie 80 tickets/jour à la main (1 h, 2 personnes). Nous proposons un
classifieur de texte (ML classique, sans LLM) : tri 60 → 10 min/jour, précision
> 85 %, cas incertains relus par un humain.
> Imprévu : la DPO limite l'analyse à l'objet des mails → précision à vérifier
> sur l'historique avant engagement (§3, §6 mis à jour).
```

## Exercice guidé

À partir de tes analyses :
1. Remplis les sections 2 à 6 du template, en tableaux quand c'est possible.
2. Après l'imprévu de 14h30, liste les sections touchées et mets-les à jour.
3. Rédige la **synthèse exécutive** (5-6 lignes + la ligne « imprévu »).
4. Relis-toi du point de vue du **client** : comprend-il en 3 minutes sans jargon ?

*Solution attendue* : 3 pages, synthèse autoportante, KPI chiffrés, imprévu visible.

## Pièges fréquents

| Piège | Conséquence |
|---|---|
| Dépasser 3 pages | Pas lu par le décideur, temps perdu |
| Jargon technique non défini | Le client décroche |
| Synthèse écrite en premier | Elle ne reflète pas les conclusions |
| Imprévu ajouté en paragraphe isolé | Sections incohérentes entre elles |
| Sobriété non argumentée | Critère manqué |
| Pas de KPI chiffrés | Cadrage non actionnable |

| Symptôme | Cause probable |
|---|---|
| Le client redemande « donc ? » | Pas de synthèse claire |
| Document trop technique | Écrit pour un dev, pas pour le persona |
| Archi ≠ contraintes du client | Imprévu non répercuté dans §5 |
| Reco LLM non justifiée | Section sobriété absente |

## Pour aller plus loin

- Pyramide de Minto (structurer) : https://en.wikipedia.org/wiki/Barbara_Minto
- Cf. M7-B1 (rapport 2 lectorats) — communication décideur.

## Vérification (checklist apprenant)

- [ ] 3 pages max, 6 sections, un seul fichier.
- [ ] Synthèse exécutive en tête (besoin + solution + KPI + imprévu).
- [ ] Lisible par le persona client (pas de jargon non défini).
- [ ] Sobriété argumentée (LLM retenu/refusé : 3 lignes).
- [ ] KPI chiffrés + questions ouvertes.

> 💡 **Récap — Document de cadrage** : 3 pages, 6 sections, un seul fichier, **synthèse exécutive en tête** (rédigée en dernier) ; tableaux plutôt que paragraphes ; imprévu client répercuté ; KPI chiffrés ; sobriété argumentée ; finir par les questions ouvertes.

### À retenir

- Le livrable se juge sur sa **clarté pour le destinataire**, pas sur sa longueur.
- **Chiffrer** plutôt qu'affirmer : un nombre vaut mieux qu'un adjectif.
- **Sobriété** : recommander le plus simple qui résout le besoin, et **dire ce qu'on écarte**.
- Distinguer ce qu'on **sait** de ce qui reste **à clarifier** (questions ouvertes).
