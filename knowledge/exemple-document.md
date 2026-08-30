---
type: Procédure
title: Reconnexion après expiration de session
description: Comment réauthentifier un poste dont la session a expiré, et ce qu'il faut vérifier avant.
tags: [authentification, sso, exploitation]
sources:
  - id: doc-editeur-sso
    resource: https://exemple.test/docs/sso/reconnexion
    title: Documentation éditeur — reconnexion SSO
    last_modified: 2026-05-30T00:00:00Z
  - id: incident-4521
    resource: "incident interne #4521"
    title: Bouton de réauthentification déplacé en 3.2
generated: { by: "human:prenom.nom", at: 2026-08-30T09:00:00Z }
verified:
  - { by: "human:prenom.nom", at: 2026-08-30T09:00:00Z }
status: stable
stale_after: 2027-02-28T00:00:00Z
---

# Reconnexion après expiration de session

Ce document est un **modèle de rédaction**. Il montre à quoi ressemble un
document conforme au schéma de cette base. Supprime-le à l'instanciation
(voir `INSTANTIATE.md`, étape 7).

## Quand cette procédure s'applique

La session expire au bout de 8 heures d'inactivité. Le symptôme est une page
blanche au retour, sans message d'erreur — ce n'est pas une panne du service.

Si l'utilisateur voit un message d'erreur explicite, ce n'est pas ce cas :
voir [les incidents connus](references/) à la place.

## Procédure

1. Fermer l'onglet, sans vider le cache du navigateur.
2. Rouvrir l'application depuis le portail interne.
3. Cliquer sur **réauthentifier**, dans le menu profil en haut à droite.[^incident-4521]
4. Vérifier que le nom d'utilisateur affiché est bien celui attendu : une
   session résiduelle d'un autre compte est la cause la plus fréquente des
   échecs de reconnexion.

> Depuis la version 3.2, le bouton **réauthentifier** n'est plus dans la barre
> supérieure mais dans le menu profil.[^incident-4521] La documentation éditeur
> n'était pas encore à jour à la dernière vérification.[^doc-editeur-sso]

## Si cela ne suffit pas

| Symptôme | Cause probable | Action |
|---|---|---|
| Boucle de redirection | Cookie de session corrompu | Vider les cookies du domaine, uniquement |
| « Compte non provisionné » | Compte absent de l'annuaire | Escalader au support identité |
| Réauthentification sans effet | Session résiduelle d'un autre compte | Déconnexion complète, puis reprendre à l'étape 1 |

## Notes de rédaction

Ce que ce modèle illustre, et qui vaut pour tout document de cette base :

- **Le frontmatter porte la traçabilité.** `sources` recense d'où vient
  l'information ; `verified` dit qui l'a confirmée et quand ; `stale_after`
  fixe la date à partir de laquelle il faudra revérifier.
- **Les affirmations datables sont attribuées** par note de bas de page,
  dont l'étiquette est un `sources[].id`. Une source réordonnée ne change
  pas l'attribution.
- **Le corps est structuré** : titres, listes numérotées, tableaux. Une
  session peut alors n'en lire qu'une section (`kb_read` avec `section`)
  au lieu du document entier.
- **Un document répond à une question qu'on se pose vraiment.** Pas de
  section « Introduction » ni « Généralités ».

[^doc-editeur-sso]: Documentation éditeur — reconnexion SSO.
[^incident-4521]: Incident interne #4521, constaté sur 3 postes le 13/06.
