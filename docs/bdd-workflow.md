# Workflow BDD et découpage des skills

Ce document explique comment utiliser les skills autour du BDD, et la différence entre `prd-to-bdd` et `implement-scenarios`.

## Ordre recommandé

1. `event-storming` — capturer le domaine et les concepts clés.
2. `grill-me` — clarifier le problème et les décisions.
3. `write-a-prd` — produire un Epic Jira avec le besoin et les user stories.
4. `ubiquitous-language` — fixer le vocabulaire canonique.
5. `prd-to-bdd` — transformer l'Epic en scénarios Gherkin et squelettes de steps.
6. `prd-to-issues` — découper l'Epic en Stories Jira liées aux scénarios.
7. `implement-scenarios` — implémenter les scénarios un par un.
8. `tdd` — servir de boucle interne pour les tests unitaires.

## Différence entre `prd-to-bdd` et `implement-scenarios`

| Skill | Rôle | Entrée | Sortie |
|---|---|---|---|
| `prd-to-bdd` | Spécification BDD | Epic Jira | `.feature` files + step skeletons |
| `implement-scenarios` | Implémentation BDD | `.feature` files | Code + tests + steps fonctionnels |

En bref : `prd-to-bdd` écrit le contrat en Gherkin, `implement-scenarios` le rend vrai.

## Flux global

```mermaid
flowchart TD
    A[event-storming] --> B[grill-me]
    B --> C[write-a-prd]
    C --> D[ubiquitous-language]
    D --> E[prd-to-bdd]
    C --> F[prd-to-issues]
    E --> G[features/*.feature]
    F --> H[Jira Stories]
    G --> I[implement-scenarios]
    I --> J[tdd]
```

## Zoom sur le BDD

```mermaid
sequenceDiagram
    participant U as User
    participant P as PRD Epic
    participant B as prd-to-bdd
    participant F as .feature files
    participant I as implement-scenarios
    participant T as tdd

    U->>P: Epic Jira
    P->>B: user stories + contexte
    B->>F: scénarios Gherkin + steps "Pending"
    U->>I: choisir un scénario
    I->>T: écrire les tests unitaires nécessaires
    T-->>I: code vert
    I-->>F: step definitions implémentées
```

## À retenir

- `prd-to-bdd` structure la discussion métier en scénarios.
- `implement-scenarios` transforme les scénarios en comportement réel.
- Les deux se complètent : l'un écrit la spec, l'autre l'implémente.
