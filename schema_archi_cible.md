# Schéma d’architecture cible — tri des mails RH

```mermaid
flowchart LR
    SRC[(Boîte RH)] --> ING[Ingestion sécurisée]
    ING --> PREP[Préparation et minimisation du message<br/>Corps du mail en v1]
    PREP --> MODEL[Classifieur supervisé<br/>6 catégories]
    MODEL --> DEC{Confiance suffisante ?<br/>Seuil renforcé pour paie}
    DEC -->|Oui| ROUTE[Routage automatique]
    ROUTE --> DEST[(Boîte de l’équipe concernée)]
    DEC -->|Non| HUM[Revue et classement manuel RH]
    HUM --> DEST

    ROUTE --> LOG[(Journal pseudonymisé<br/>Catégorie, destination, horodatage)]
    HUM --> LOG
    LOG --> MON[Suivi des indicateurs<br/>Reclassements, catégorie « autres », performance]
```

**Composants** : boîte RH, ingestion sécurisée, préparation du message, classifieur supervisé, contrôle de confiance, routage ou revue manuelle, boîtes des équipes, journal pseudonymisé et suivi des indicateurs.

**Éléments écartés en v1** : LLM et API externe, car un classifieur supervisé répond au besoin avec les tickets labellisés disponibles et évite l’exposition aux injections de consignes. Pas de RAG ni de base vectorielle, inutiles pour le routage. Les pièces jointes ne sont pas analysées en v1 ; ce périmètre reste à confirmer avec le client.
