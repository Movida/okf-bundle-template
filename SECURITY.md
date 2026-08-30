# Sécurité

Ce dépôt ne contient **aucun code exécutable** : c'est un modèle de fichiers
markdown et YAML. Il n'a pas de surface d'attaque propre.

## Ce qui compte quand même

**Un bundle instancié depuis ce template sera lu par des sessions Claude.**
Trois de ses fichiers finissent dans le contexte d'un modèle :

- `okf-bundle.yaml` — `title` et `description` sont injectés dans les
  descriptions d'outils MCP, donc dans le contexte de **toutes les sessions
  connectées au hub**, sans que quiconque ouvre le bundle ;
- `GOVERNANCE.md` — dans le contexte du gestionnaire à chaque revue ;
- `CLAUDE.md` — dans celui de toute session ouvrant le dépôt.

Conséquences pratiques :

- **Ne mettez aucun secret dans un corpus.** Identifiants, jetons, URL internes
  authentifiées : rien de tout cela n'a sa place dans une base de connaissance.
  Un bundle n'est pas un coffre.
- **N'importez que des bundles de confiance**, et relisez leur manifeste,
  `GOVERNANCE.md` et `CLAUDE.md` avant le premier usage. Importer un bundle est
  sans risque d'exécution, mais pas sans risque d'influence.

Le modèle de menace complet du système est dans le dépôt du hub :
[`SECURITY.md`](https://github.com/Movida/okf-hub/blob/main/SECURITY.md).

## Signaler

Pour une vulnérabilité touchant le hub lui-même, utilisez les advisories privées
du dépôt `okf-hub`, pas une issue publique.
