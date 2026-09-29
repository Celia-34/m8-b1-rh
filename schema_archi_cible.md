# Schéma d’architecture cible — tri des mails RH

```mermaid
flowchart LR
    SRC[(Outil de ticketing)] --> ING[Ingestion sécurisée]
    ING --> PREP[Extraction et minimisation de l'objet<br/>Corps et pièces jointes exclus]
    PREP --> MODEL[Classifieur<br/>6 catégories]
    MODEL --> DEC{Objet reconnu / confiance suffisante ?<br/>Seuil renforcé pour paie}
    DEC -->|Oui| ROUTE[Routage automatique]
    ROUTE --> DEST[(Boîte de l’équipe concernée)]
    DEC -->|Non| HUM[Revue et classement manuel RH]
    HUM --> DEST

    ROUTE --> LOG[(Journal pseudonymisé<br/>Catégorie, destination, horodatage<br/>Sans objet brut)]
    HUM --> LOG
    LOG --> MON[Suivi des indicateurs<br/>Reclassements, catégorie « autres », performance]
```

**Composants** : ticketing, extraction de l’objet, classifieur, contrôle, routage ou revue, journal et suivi.

**Choix à confirmer** : objets préformattés par l'outil de ticketting. Format et suffisance à valider.

**Écartés en v1** : corps, pièces jointes, LLM, API externe, RAG et base vectorielle. L’objet peut contenir des données personnelles : ne pas le conserver dans les journaux.
