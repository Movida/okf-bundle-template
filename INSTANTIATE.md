# Instancier ce template

Cette checklist est conçue pour être **déroulée par une session Claude qui
interroge l'humain**. Si tu es cette session : pose les questions dans l'ordre,
une par une, attends la réponse, et n'invente aucune valeur par défaut sur les
points marqués « demander ». Quand tout est rempli, supprime ce fichier du dépôt
instancié — il n'a plus d'objet.

Si tu es un humain qui préfère faire à la main : les mêmes étapes se suivent
très bien seul.

---

## 1. Identité de la base

**Demander :** de quoi cette base parle-t-elle, en une ou deux phrases ?
En creux, qu'est-ce qui n'y a explicitement pas sa place ?

Déduire de la réponse, puis **faire valider** :

- `name` — identifiant technique, motif `[a-z0-9-]+`. C'est la valeur que les
  outils MCP attendront en paramètre `base`. Court et sans ambiguïté :
  `solution-editeur-x`, pas `base` ni `kb`.
- `title` — nom lisible, ≤ 100 caractères, une seule ligne.
- `description` — 1 à 3 phrases. **Rédige-la pour le routage** : elle sera
  injectée dans les descriptions d'outils MCP de toutes les sessions connectées
  au hub, et c'est sur elle qu'un agent décidera d'interroger cette base plutôt
  qu'une autre. « Documentation de X » ne suffit pas ; dis ce qu'on y trouve.

Reporter les trois valeurs dans `okf-bundle.yaml`, et le `title` dans le titre
de `GOVERNANCE.md`.

## 2. Périmètre

**Demander :** cite deux ou trois choses qui appartiennent clairement à cette
base, et deux ou trois qui n'y appartiennent pas.

Remplacer les placeholders de la section « Périmètre » de `GOVERNANCE.md` par
ces exemples concrets. Des exemples réels valent mieux qu'une définition
abstraite : c'est sur eux que le gestionnaire calera son jugement.

## 3. Golden rules

Le template propose six règles de départ. Les passer en revue avec l'humain :

**Demander, pour chacune :** celle-ci convient-elle telle quelle ?

Puis : **y a-t-il une règle propre à ce domaine ?** (règle 7). Exemples de ce
qui remonte souvent : « toute procédure indique la version du produit sur
laquelle elle a été vérifiée », « aucune capture d'écran, elles périment trop
vite », « les incidents sont datés et portent leur numéro de ticket ».

## 4. Organisation du corpus

**Demander :** comment veux-tu ranger les documents ? Par domaine
fonctionnel ? par produit ? par type (procédures / incidents / références) ?

Créer les sous-répertoires correspondants sous `knowledge/`, et mettre à jour
l'arborescence donnée dans la section « Organisation du corpus » de
`GOVERNANCE.md`. Ne pas créer de répertoire « au cas où » : un répertoire vide
est du bruit pour la recherche comme pour la lecture.

## 5. Style

**Demander :** langue du corpus ? tutoiement ou vouvoiement dans les
procédures ? y a-t-il un glossaire ou des conventions de nommage existants à
respecter ?

Reporter dans la section « Style et conventions » de `GOVERNANCE.md`.

## 6. Schéma de frontmatter

**Demander :** quelles valeurs de `type` vas-tu réellement utiliser ?

Les lister dans le champ `type` de `schema.yaml`. Puis proposer, sans imposer :
« veux-tu suivre la fraîcheur des documents ? » — si oui, garder `verified` et
`stale_after` ; si non, les retirer du schéma plutôt que les laisser inutilisés,
ce qui égarerait le gestionnaire.

## 7. Premier document

**Demander :** quel est le premier vrai sujet à documenter ?

Écrire ce document dans `knowledge/`, en suivant le schéma retenu, et
supprimer `knowledge/exemple-document.md`. Un template livré avec son document
d'exemple encore en place produit une base dont le premier résultat de
recherche est du remplissage.

Mettre à jour `knowledge/index.md` et `knowledge/log.md` en conséquence.

## 8. Finalisation du dépôt

```sh
# Renommer le remote si le dépôt vient d'un clone du template
git remote remove origin      # ou : git remote set-url origin <ton-url>

rm INSTANTIATE.md
git add -A
git commit -m "Instanciation de la base <name>"
```

## 9. Déploiement sur le hub

```sh
cd <racine-du-hub>
git clone <url-du-bundle> bases/<name>
```

Puis, depuis une session connectée au hub, appeler l'outil `kb_hub_rescan`.

**Rappeler à l'humain :** le rescan n'a d'effet que sur la session qui
l'exécute. Les autres sessions Claude déjà ouvertes sur ce hub ne verront la
nouvelle base qu'après leur propre rescan, ou après redémarrage.

## 10. Vérification

Depuis une session connectée :

- `kb_list` → la base apparaît, avec son titre, sa description et son nombre de
  documents ;
- `kb_governance` avec `base: <name>` → les golden rules et le schéma sortent ;
- `kb_search` sur un mot du premier document → il est trouvé ;
- `kb_propose` avec une proposition d'essai → elle atterrit dans
  `proposals/pending/` et un commit `proposal: …` apparaît dans le dépôt.

Résoudre ensuite la proposition d'essai avec la skill `kb-review`, pour vérifier
le cycle complet avant d'ouvrir la base à des contributeurs.
