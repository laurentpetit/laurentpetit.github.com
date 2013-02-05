---
layout: post
title: "Code Story, Clojure et moi"
date: 2013-02-04 00:11
comments: true
categories:
---

Cet article est le premier d'une série visant à présenter le langage [Clojure](http://www.clojure.org) via l'implémentation d'une solution _tout Clojure_ au challenge CodeStory.

C'est à quel sujet ?
====================
J'ai eu le plaisir de participer et me qualifier à la première phase du concours de programmation [Code Story 2013](http://code-story.net/2013/01/04/concours-2013.html).

Pour y parvenir **j'ai choisi d'utiliser le langage [Clojure](http://www.clojure.org)**.

Je voulais apporter un peu d'exotisme en utilisant la **programmation fonctionnelle**, pour changer un peu de toutes les contributions qui allaient utiliser le même paradigme impératif (Java, Kotlin, Ceylon, Groovy, Scala, etc.).

> Ce premier article se concentre sur quelques caractéristiques du concours, et pourquoi Clojure est un langage de choix pour les adresser

Web Services
============
Pour participer à l'épreuve, il fallait mettre en place un serveur Web. **Toutes les questions, y compris les énoncés, ont été envoyées par HTTP GET ou POST.**

[Ring](https://github.com/ring-clojure/ring) est la librairie standard Clojure pour écrire des applications Web. C'est une abstraction "minimaliste" (mais pas simpliste !) d'un serveur web.

> Clojure+Ring pour faire une appli Web : c'est simple, lisible, concis

TDD
===
Le déroulement des épreuves imposait un format analogue à la méthodologie `TDD` (Test-Driven Development) :

- Envoi d'un test en boucle sur nos serveurs, jusqu'à obtention d'une réponse correcte
- Complexification incrémentale des tests envoyés

Dans ces conditions, il n'est pas rare (ni anormal) d'avoir à réécrire de grandes portions de code.
*Une étape de refactoring entre chaque nouveau test est généralement nécessaire en TDD*

**Il est naturel d'adopter l'approche TDD en Clojure**, car le langage :

- **Facilite l'écriture des tests** : les tests sont concis, lisibles, faciles à refactorer.
- **Facilite l'écriture du code** : écrire du nouveau code en Clojure est une danse entre l'éditeur et l'environnement dynamique d'exécution. Tout nouveau code est façonné / testé dans l'environnement d'exécution. Imaginez le remplacement à chaud du mode Debug de votre IDE, *"on steroïds"*.
- **Favorise le refactoring** : le code Clojure est généralement très concis. Souvent 3 à 10 fois plus concis que son équivalent Java, par exemple. La masse de code à modifier fait moins peur. De plus, l'unité de réutilisation de code étant la fonction, et non la classe, le code est naturellement plus facile à refactorer.

> Clojure pour faire du TDD, c'est efficace, lisible, simple, concis

Performances
============
Le dernier exercice du concours a soumis nos méninges à rude épreuve. Il ne suffisait pas d'avoir un code qui fonctionne, il fallait trouver un code "performant".

Mais pas _"Performant"_ comme dans "comment gagner quelques microsecondes dans l'exécution d'une requête portant sur quelques éléments à traiter". NON. _"Performant"_ comme dans "écrire un algorithme pouvant traiter une requête portant sur plusieurs centaines de milliers, ou des millions, d'éléments".

Pour cette épreuve, écrire un algorithme récursif "naïf", puis tenter des optimisations locales dessus, c'était un peu comme être sur le Titanic pendant le naufrage, à s'acharner à graisser les portes de la salle de réception. Ça occupe, mais ça ne sert à rien. Au-delà de 100 entrées, un algo "naïf" prenait déjà plusieurs dizaines de secondes. **Pour CodeStory, il fallait être capable de traiter des requêtes de 50.000 éléments ou plus** ! On attend toujours que les algorithmes récursifs aient fini de répondre ... ([pauvres chatons](https://twitter.com/CodeStory/status/297268190566813696))

> Pour être honnête, sur ce genre de problème, le langage de programmation importe peu

Si vous n'avez pas le bon algorithme, aucun langage ni aucun ordinateur si puissant soit-il ne vous viendra en aide : vous n'y arriverez pas.
Un algorithme de complexité algorithmique est quasi linéaire (dont le temps de réponse est proportionnel, ou légèrement proportionnel au nombre d'éléments à traiter) l'emportera haut la main sur n'importe quel algorithme exponentiel, et ce très rapidement (dès que la taille du problème dépassera quelques dizaines d'éléments).

Là encore, j'aimerais souligner les **caractéristiques de Clojure qui ont facilité la résolution de ce problème**:

- **Facilité de prototypage** : la librairie de base de Clojure est riche en fonctions de manipulation de collections. Les sort, group-by, max-key, etc. y sont presque toutes !
- **Facilité de refactoring** : le code produit restant concis, il est facile de le refactorer, d'en produire une version différente. Le fait de manipuler des fonctions plutôt que des classes est un accélérateur de ce phénomène.
- **Code performant** : à algorithme identique, il reste important que le langage utilisé ne soit pas extrêmement plus lent que les langages "concurrents". En utilisant du Clojure "idiomatique", sans chercher à optimiser, sans compromettre la lisibilité (sous réserve de connaître Clojure et les fonctions standards utilisées, oeuf de course), le code produit s'est avéré du même ordre de grandeur que les solutions concurrentes. En moyenne seulement 2, parfois 3 fois moins rapide. Il serait possible d'optimiser pour aller "talonner" les langages impératifs (utilisation de tableaux, par ex.), mais c'était juste non requis, donc non nécessaire.


C'est tout pour aujourd'hui
===========================

Si ce premier article vous a mis l'eau à la bouche, et que vous souhaitez que je continue la série avec des articles techniques et du code, envoyez-moi un petit mot d'encouragement :-).

Merci de m'avoir lu.

