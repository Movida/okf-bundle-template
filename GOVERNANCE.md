---
# draft | stable — défaut si absent : stable.
# Un template est livré en brouillon : les règles ci-dessous sont des
# exemples que personne n'a encore validés pour TA base. Passe à `stable`
# à l'étape 8 d'INSTANTIATE.md, une fois les golden rules arbitrées.
status: draft
---

# Gouvernance — <Nom lisible de la base>

Ce document est injecté dans le contexte du gestionnaire à chaque revue de
propositions. Il est lu par une session Claude : écris-le comme des consignes
opérationnelles, pas comme une charte. Chaque règle doit être **décidable** —
si tu ne peux pas dire, en la lisant, si une proposition donnée passe ou non,
elle est trop vague.

## Périmètre

**Appartient à cette base :**

- <ex. : la configuration, l'exploitation et les incidents connus de la solution X>
- <ex. : les procédures internes qui dépendent de X>

**N'appartient PAS à cette base :**

- <ex. : la documentation éditeur amont — on la référence par URL, on ne la recopie pas>
- <ex. : tout ce qui concerne la solution Y : elle a sa propre base>
- <ex. : les secrets, identifiants, jetons — jamais, sous aucune forme>

Une proposition hors périmètre est rejetée avec le motif « hors périmètre »,
en indiquant, si elle existe, la base où elle aurait sa place.

## Golden rules d'intégration

Ces règles sont contraignantes pour le gestionnaire.

1. **Sources exigées.** Toute affirmation factuelle doit porter au moins une
   source vérifiable : URL, numéro d'incident, référence de ticket, ou constat
   terrain daté et localisé. Une proposition sans source exploitable est
   rejetée, pas escaladée.

2. **Confiance et corroboration.** Une proposition `confidence: low` n'est
   jamais intégrée seule : il lui faut une seconde source indépendante, ou une
   corroboration par un document existant. Sinon, escalade à l'humain.

3. **Contradiction avec l'existant.** Une proposition qui contredit un document
   du corpus n'est jamais intégrée par simple écrasement. Le gestionnaire
   présente les deux versions et leurs sources respectives à l'humain, et
   attend l'arbitrage.

4. **Doublons.** Deux propositions sur le même sujet se résolvent dans un seul
   commit : la mieux sourcée est intégrée, l'autre rejetée avec le motif
   « doublon de <id> ».

5. **Propositions de type `question`.** Elles ne portent pas de réponse. Le
   gestionnaire enquête dans le corpus et propose une réponse sourcée, ou
   rejette avec un motif, ou escalade. Jamais d'intégration telle quelle.

6. **Portée du changement.** Une intégration modifie le strict nécessaire.
   Réorganiser un document, en renommer un autre ou corriger un style au
   passage n'est autorisé que sur instruction humaine explicite.

7. **<Ajoute ici les règles propres à ton domaine.>**
   <ex. : toute procédure doit indiquer la version du produit sur laquelle elle
   a été vérifiée>

## Organisation du corpus

<Décris la structure réelle, pas une structure idéale. Le gestionnaire s'en
sert pour décider où ranger une addition.>

```
knowledge/
├── index.md              # sommaire du bundle (convention OKF)
├── log.md                # historique des mises à jour (convention OKF)
├── <domaine-a>/
│   ├── index.md
│   └── <sujet>.md
└── references/           # matériel externe recopié, scripts, captures
```

- Un document = un sujet. Si un document dépasse <ex. : 400 lignes>, il se scinde.
- Nommage des fichiers : <ex. : `kebab-case`, en français, sans date>.
- Un nouveau domaine (nouveau sous-répertoire) ne se crée que sur instruction
  humaine.

## Style et conventions

- **Langue :** <français / anglais>. Une seule langue dans tout le corpus.
- **Ton :** opératoire. On écrit ce qu'il faut faire et ce qui se produit, pas
  des considérations générales.
- **Format :** markdown structuré — titres, listes, tableaux, blocs de code.
  On évite les longs paragraphes : ils se recherchent et se citent mal.
- **Granularité :** un document doit répondre à une question qu'on se pose
  réellement.
- **Datation :** toute affirmation susceptible de périmer porte sa date de
  vérification dans le frontmatter (voir `schema.yaml`).

## Identité du relecteur

En mode `review: human`, le trailer `Reviewed-By:` du commit porte l'identité
de l'humain qui confirme, sous la forme `human:<id>` (convention d'acteur OKF).
