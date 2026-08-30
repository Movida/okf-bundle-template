# Contribuer au template

Ce dépôt n'est pas une base de connaissance : c'est le **modèle** dont on part
pour en créer une. Contribuer ici, c'est améliorer ce que trouvera la prochaine
personne qui instancie une base.

## Ce qui est utile

- **Rendre une règle plus décidable.** Une golden rule d'exemple dont on ne peut
  pas dire, en la lisant, si une proposition donnée passe ou non, est une
  mauvaise règle d'exemple — même si elle est bien écrite.
- **Une question manquante dans `INSTANTIATE.md`.** Si vous avez instancié une
  base et buté sur un choix que le questionnaire ne posait pas, c'est le
  signalement le plus précieux.
- **Corriger le résumé OKF de `CLAUDE.md`** si la spécification amont évolue.
  Elle est en v0.2 aujourd'hui.

## Ce qui ne l'est pas

- Du contenu de domaine. Le document d'exemple existe pour montrer une **forme**
  de rédaction ; il est supprimé à l'instanciation. L'enrichir ne sert personne.
- Des placeholders plus nombreux. Un template qu'on passe une heure à vider est
  un template raté.

## Vérifier une modification

Instanciez-le pour de vrai, et déployez-le :

```sh
git clone <ce-dépôt> essai && cd essai
rm -rf .git && git init -b main
# dérouler INSTANTIATE.md
cd <racine-du-hub> && git clone <chemin-de-essai> bases/essai
```

Puis, depuis une session connectée au hub : `kb_hub_rescan`, `kb_list`,
`kb_governance`, `kb_search`, et un `kb_propose` d'essai. Si l'une de ces étapes
demande une manipulation non prévue par `INSTANTIATE.md`, c'est le template qu'il
faut corriger.

## Licence

En contribuant, vous acceptez que votre contribution soit distribuée sous la
licence [Apache 2.0](LICENSE) du projet.
