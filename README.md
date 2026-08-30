# okf-bundle-template

Template de **bundle** pour le [OKF Bundle Hub](https://github.com/Movida/okf-hub) : un dépôt git
contenant un corpus markdown, son manifeste et ses règles de gouvernance.

Un bundle se lit sans le hub — c'est un répertoire de markdown, `cat` suffit.
Le hub n'ajoute que l'accès par des sessions Claude isolées et le circuit de
propositions.

## Utiliser ce template

```sh
git clone <url-de-ce-template> ma-base
cd ma-base
rm -rf .git && git init -b main
```

Puis ouvre une session Claude dans le dépôt et demande-lui de dérouler
[INSTANTIATE.md](INSTANTIATE.md) — c'est un questionnaire d'instanciation conçu
pour être exécuté par un agent qui t'interroge. À la main, la même checklist se
suit très bien seul.

## Contenu

| Fichier | Rôle |
|---|---|
| `okf-bundle.yaml` | Manifeste. Sa présence fait de ce dépôt un bundle. **Obligatoire.** |
| `GOVERNANCE.md` | Périmètre et golden rules d'intégration. **Obligatoire.** |
| `schema.yaml` | Champs de frontmatter attendus. Documentaire en v0. |
| `CLAUDE.md` | Contexte pour toute session ouvrant le dépôt, dont la règle « ne jamais modifier le corpus hors circuit de propositions ». |
| `INSTANTIATE.md` | Checklist d'instanciation. À supprimer une fois déroulée. |
| `knowledge/` | Le corpus. Nom réglable par `corpus-dir` du manifeste. |

Le répertoire `proposals/` n'est pas versionné dans le template : il est créé
automatiquement au premier dépôt de proposition.

## Déployer

```sh
cd <racine-du-hub>
git clone <url-de-ma-base> bases/<name>
```

Puis `kb_hub_rescan` depuis une session connectée. Rien d'autre.

## Licence

[Apache 2.0](LICENSE). Voir [`NOTICE`](NOTICE).

Une base instanciée depuis ce template **n'hérite pas de cette licence** : le
corpus que vous y écrivez est le vôtre, et vous le licenciez comme vous
l'entendez. Pensez-y avant de publier une base dont le contenu reprend de la
documentation tierce.
