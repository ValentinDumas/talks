## Le dilemme du code legacy : on maintient ou on réécrit ?



### Abstract

Avez-vous déjà été confronté à l'anxiété de travailler dans une base de code legacy, craignant que même un changement mineur ne provoque des erreurs en cascade ? Évitez-vous de toucher à certaines parties du code parce que les tests vous semblent être des obstacles fragiles plutôt que des filets de sécurité ? Vous n'êtes pas seul.

Le code legacy n'est souvent pas accompagné de tests propres, et lorsque des tests sont présents, ils peuvent être fragiles, incomplets ou trop complexes. Comment retrouver la confiance et rompre ce cycle de prudence et de confusion ? Comment transformer les tests en un outil d’automatisation plutôt qu'en une source de frustration ?

Dans cette conférence, je partagerai avec vous quelques techniques concrètes pour identifier les zones à risque et rendre le code existant plus robuste et plus clair grâce à des stratégies de refonte et de test ciblées.

Le tout en live coding !



### Talk references

L'objectif de ce talk est de proposer, à travers des cas concrets d'utilisation incrémentale, des approches pour donner des clés et faire évoluer la vision des tests de codes legacy d'un obstacle frustrant à un outil puissant pour faire évoluer en toute confiance des bases de codes complexes, tout en limitant la dette et les bugs.

Au travers d'exemples pratiques, je montrerai comment :

notre réflexion impacte les DORA metrics.
Identifier les zones à haut risque et les cibler avec une couverture de test stratégique.
Construire des suites de tests robustes avec un mélange de tests unitaires et de tests d'intégration adaptés.
Transformer le code hérité en systèmes stables et faciles à maintenir qui encouragent le remaniement en toute sécurité. Nous discuterons de techniques spécifiques qui non seulement renforcent la confiance dans les tests, mais soutiennent également de meilleures décisions de conception et permettent aux développeurs de faire évoluer leur code sans hésitation. Ces techniques proviennent de nombreux articles et livres que j'ai lus, de « Working Effectively with Legacy Code - Michael Feathers » aux livres de Kent Beck sur les tests.
Je conclurai par les principaux enseignements à tirer :

Les gains de temps et de productivité significatifs d'une stratégie de test efficace.
La manière dont des tests fiables débloquent des améliorations architecturales plus sûres.
Un rappel de la valeur qu'une suite de tests fiable apporte à tout développeur confronté à un code hérité.
Le public aura accès à des échantillons de code Github et à un logigramme que j'ai créé (à partir de mes lectures personnelles) pour aider les développeurs à décider quelle technique utiliser dans un contexte et une configuration spécifiques.