---
# You can also start simply with 'default'
theme: seriph
titleTemplate: '%s - Valentin Dumas'
fonts:
  sans: DM Sans
  serif: Noto Serif
  mono: Consolas
addons:
  - slidev-addon-graph
background: https://images.unsplash.com/photo-1716406536069-c27068316336?q=80&w=2081&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# some information about your slides (markdown enabled)
title: "Le dilemme du Code Legacy: on maintient ou on réécrit ?"
info: |
  ## Slidev Starter Template
  Presentation slides for developers.
class: text-center
drawings:
  persist: false
transition: fade
mdc: true
---

# Le dilemme du code legacy

## Maintenir ou Réécrire ?

<div class="abs-br m-6 text-xl">
  <span class="text-xs m-x-3 text-white/60">Valentin Dumas</span>
  <a href="https://github.com/ValentinDumas/talks" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
  <a href="https://www.linkedin.com/in/valentindumas" target="_blank" class="slidev-icon-btn">
    <carbon:logo-linkedin />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: slide-left
layout: cover
background: /case-study-equifax/equifax.webp
---

<!--

Equifax est une entreprise spécialisée dans les données de crédit : elle collecte, analyse et vend des informations financières sur les consommateurs à des banques, assureurs et employeurs pour évaluer leur solvabilité.

En 2017, L’agence américaine d’analyse de crédit Equifax a subi l'une des plus grandes violations de données de l'histoire, exposant les informations personnelles d'environ 147 millions de personnes, y compris les noms, les numéros de sécurité sociale, les dates de naissance, les adresses et, dans certains cas, les numéros de permis de conduire et de carte de crédit. La violation s'est produite entre la mi-mai et juillet 2017 et n'a été découverte qu'à la fin du mois de juillet.

-->

---
transition: slide-left
layout: center
#layout: image
#image: https://images.unsplash.com/photo-1572883454114-1cf0031ede2a?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
---

# Causes de la faille

<div class="text-xl opacity-80 p-2">

  <!-- https://www.blackduck.com/blog/cve-2017-5638-apache-struts-vulnerability-explained.html -->
  📝 **(CVE-2017-5638)** dans **Apache Struts** : Correctif en mars 2017, non appliqué
  <br><br>

  🧑‍💻 **Corrections tardives** : Audit infructueux, certificats TLS expirés, complexité de code
<br><br>

  🤹 Pas de **segmentation réseau**:  Accès aux bases de données sur l'ensemble du réseau
<br><br>

  🛠 **Aucune limite** de requête BDD:  Extraction de données sensibles sans détection
  <!-- note: peut suggérer un manque de tests -->
  <!-- note: sur des données sensibles comme ça, on peut emettre des réserves sur les requetes de récupération -->

</div>

<style>
strong, h1 {
  color: #2B90B6;
}
</style>

<!--
Causes

https://www.blackduck.com/blog/cve-2017-5638-apache-struts-vulnerability-explained.html

Vulnérabilité logicielle non corrigée : Les attaquants ont exploité une vulnérabilité connue (CVE-2017-5638) dans Apache Struts, un cadre d'application web populaire. Un correctif pour cette vulnérabilité a été publié en mars 2017, mais Equifax ne l'a pas appliqué à ses systèmes.

Mauvaises pratiques de sécurité : Equifax a stocké les informations d'identification des administrateurs en clair et n'a pas utilisé d'authentification à deux facteurs pour les systèmes critiques, ce qui a facilité l'escalade de l'accès des attaquants une fois qu'ils étaient à l'intérieur.

Certificat de sécurité expiré : Les outils de surveillance du réseau d'Equifax n'ont pas détecté la violation pendant des mois parce qu'un certificat TLS clé avait expiré, empêchant l'inspection du trafic crypté.

Absence de segmentation du réseau : Les attaquants ont pu se déplacer latéralement au sein du réseau, accédant à d'autres bases de données après la violation initiale.

Aucune limite de requête : Aucune restriction n'a été imposée sur le nombre de requêtes de la base de données, ce qui a permis aux attaquants d'extraire d'importants volumes de données sans déclencher d'alertes.

note: peut suggérer un manque de tests
note: sur des données sensibles comme ça, on peut emettre des réserves sur les requetes de récupération

-->

---
transition: slide-left
layout: center
#layout: image
#image: https://images.unsplash.com/photo-1572883454114-1cf0031ede2a?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
class: text-xl opacity-80
---

# Ce qui aurait pu fonctionner ?

<div class="text-xl p-2">

  🪲 Appliquer les correctifs **dès leur publication**
  <br><br>

  🔐 Renforcer l'authentification : **authentification forte** et **multifactorielle** pour tous les accès administratifs
  <br><br>

  📊 **Monitorer** et limiter les **requêtes** BDD : requêtes excessives
  <br><br>

  💡 **Amélioration continue** sur les process et les méthodes de développement

</div>

<style>
strong, h1 {
  color: #2B90B6;
}
</style>

<!--

  Gestion des correctifs en temps opportun : Il est essentiel d'appliquer les correctifs de sécurité dès qu'ils sont publiés, en particulier pour les applications anciennes qui ne sont peut-être pas maintenues activement, mais qui traitent encore des données sensibles.

Analyse complète des vulnérabilités : Utiliser plusieurs outils d'analyse indépendants et des processus de validation pour s'assurer que tous les systèmes, y compris les anciens, sont vérifiés pour détecter les vulnérabilités connues.

Renforcer l'authentification : Exiger une authentification forte et multifactorielle pour tous les accès administratifs, et ne jamais stocker les informations d'identification en clair.

Segmentation adéquate du réseau : Limiter la capacité des attaquants à se déplacer latéralement en segmentant les réseaux et en restreignant l'accès entre les systèmes, en particulier pour les applications existantes.

Gestion des certificats et du chiffrement : Renouveler et surveiller régulièrement les certificats de sécurité afin de conserver une visibilité sur le trafic crypté et de détecter toute activité suspecte.

Limiter les requêtes dans les bases de données : Mettre en place des contrôles pour détecter et bloquer les requêtes anormales ou les extractions excessives de données, qui peuvent être le signe d'une violation en cours.

Donner la priorité à la sécurité des systèmes existants : Les applications et bases de code existantes sont souvent négligées mais peuvent constituer des points critiques de défaillance. Examinez régulièrement, mettez à jour et, si possible, remplacez ou mettez hors service les systèmes existants pour minimiser les risques.

-->

---
name: Présentation
layout: statement
class: opacity-80
---

<div class="flex flex-col justify-center items-center gap-3">
  <img src="/profile.jpg" alt="profile picture" class="h-50 rounded-100"/>
  <div class="pl-4 text-xl"><strong>Valentin DUMAS</strong></div>
  <div class="pl-4 text-sm">Ingénieur logiciel</div>
  <img src="/logo-takima.png" alt="Logo Takima" class="h-10 pl-4 pt-2" />
</div>

---
transition: slide-up
layout: statement
class: text-4xl opacity-80
---

❝ Legacy code is simply code **without tests** ❞

<span class="text-base text-gray-500">— Michael Feathers</span>

<!-- ... -->

<style>
strong {
  color: #2B90B6;
}
</style>

---
transition: slide-up
layout: statement
class: text-4xl opacity-80
---

❝ Legacy code is **valuable** code
<br>
<br>

you're **afraid** to change ❞

<span class="text-base text-gray-500">— Nicolas Carlo & Alex Bolboaca</span>

<!-- ... -->

<style>
strong {
  color: #2B90B6;
}
</style>

---
transition: slide-left
layout: default
---

<!-- TODO: probablement remplacer par un exemple de ton exercice de use case -->
```java [Extrait du Gilded Rose refactoring Kata] {*}{lines:true, maxHeight:'50vh'}
public void updateQuality() {
        for (int i = 0; i < items.length; i++) {
            if (!items[i].name.equals("Aged Brie")
                    && !items[i].name.equals("Backstage passes to a TAFKAL80ETC concert")) {
                if (items[i].quality > 0) {
                    if (!items[i].name.equals("Sulfuras, Hand of Ragnaros")) {
                        items[i].quality = items[i].quality - 1;
                    }
                }
            } else {
                if (items[i].quality < 50) {
                    items[i].quality = items[i].quality + 1;

                    if (items[i].name.equals("Backstage passes to a TAFKAL80ETC concert")) {
                        if (items[i].sellIn < 11) {
                            if (items[i].quality < 50) {
                                items[i].quality = items[i].quality + 1;
                            }
                        }

                        if (items[i].sellIn < 6) {
                            if (items[i].quality < 50) {
                                items[i].quality = items[i].quality + 1;
                            }
                        }
                    }
                }
            }

            if (!items[i].name.equals("Sulfuras, Hand of Ragnaros")) {
                items[i].sellIn = items[i].sellIn - 1;
            }

            if (items[i].sellIn < 0) {
                if (!items[i].name.equals("Aged Brie")) {
                    if (!items[i].name.equals("Backstage passes to a TAFKAL80ETC concert")) {
                        if (items[i].quality > 0) {
                            if (!items[i].name.equals("Sulfuras, Hand of Ragnaros")) {
                                items[i].quality = items[i].quality - 1;
                            }
                        }
                    } else {
                        items[i].quality = items[i].quality - items[i].quality;
                    }
                } else {
                    if (items[i].quality < 50) {
                        items[i].quality = items[i].quality + 1;
                    }
                }
            }
        }
    }
```

<!--
  Imagine un matin, tu arrives au bureau et quand tu ouvres ton IDE la première chose que tu vois c’est ça:

  **Montrer code** Vous arrivez à lire ce code ?.. Vous êtes forts.
  ** Expliquer code rapidement, ses défauts, ce qui peut être amélioré**
  ** montrer le code simplifié**

  Plusieurs challenges, dont un code domaine/métier qui peut s’avérer:
  complexe
  peu lisible

  On peut aussi parler de code enchevêtré, spaghetti, BBofMud, …

  **Montrer le plat de pâtes**
  Quand vous codez un soft, vous voyez le plat de pâtes.
  Vos relecteurs, et même vous-même après quelques mois sans relire le code = ce que vous voyez est magique.
  complexité visuelle → peu lisible

  A cette complexité s’ajoute ceci.
-->

---
name: Enjeux et Challenges du code legacy
transition: slide-left
layout: two-cols
---

# Un peu de legacy
Enjeux et challenges

<div class="flex flex-col gap-6 p-10 justify-center">
  <!-- Ligne 1 -->
  <div class="flex gap-8 items-center">
    <img v-click="1" src="/icons/project-with-deadlines.png" alt="Planning" class="h-24" />
    <img v-click="2" src="/icons/person-with-idea.png" alt="Dev" class="h-20" />
    <img v-click="3" src="/icons/debt.png" alt="Debt" class="h-20" />
  </div>
  <!-- Ligne 2 -->
  <div v-click="4" class="flex gap-8 items-center">
    <img src="/icons/code.png" alt="Code" class="h-20" />
    <span v-mark="4" class="text-xl">&gt; 100k lignes</span>
  </div>
  <!-- Ligne 3 -->
  <div v-click="5" class="flex gap-8 items-center">
    <img src="/icons/database.png" alt="Database" class="h-20" />
    <img src="/icons/cloud.png" alt="Cloud" class="h-20" />
  </div>
</div>

::right::

<div v-click="6" class="w-full h-full flex justify-center items-center">
<img src="/dependency-issues.jpg" class="h-100" alt="Dependency issues" />
</div>

---
name: Enjeux et Challenges du code legacy pt. 2
transition: slide-left
layout: two-cols
class: opacity-80
---

# Un peu de legacy
Enjeux et challenges

<div class="flex flex-col gap-6 justify-center">
  <img src="/icons/kapla-tower-beautiful.png" class="h-100" alt="Dependency issues" />
</div>

::right::

<div class="w-full h-full flex flex-col justify-center items-center py-25">
  <!-- Ligne 1 -->
  <div class="flex gap-8 items-center">
    <img v-click src="/icons/kapla-tower-instable.png" alt="Kaplar Tower Instable" class="w-60" />
    <img v-click src="/icons/mikado.png" alt="Mikado" class="w-45" />
  </div>
  <!-- Ligne 2 -->
  <div v-click class="flex gap-8 items-center">
    <img src="/icons/bonhomme-tire-pelote.png" alt="Code" />
  </div>
</div>

<!-- notes -->


---
transition: slide-up
layout: statement
class: text-4xl
---

❝ Tout code **deviendra legacy** ❞

<style>
strong {
  color: #2B90B6;
}
</style>

<!--

“Avoir un code Legacy n'est pas un échec, ça prouve que l'application a eu du succès dans le temps, malgré la dette technique. De toute façon n'importe quel code, aussi beau soit-il écrit aujourd'hui sera le Legacy de demain. Il est quand même important de revenir régulièrement pour rafraîchir le code et enlever progressivement de la dette technique.” explique Gabriel Pillet, CTO chez Web^ID.

Effectivement, il y a 3 types de code legacy :
- Le code qui a été soigné par ses prédécesseurs. Il est clair, commenté, testé et donc facilement maintenable (mais cela n’est pas le cas le plus fréquent !).
- Le code difficilement maintenable. Il n’est pas très lisible au premier coup d’œil, il contient du code mort ou dupliqué, il y a des classes trop grandes, il y a peu, voire pas de tests unitaires, etc.
- Le code obsolète. C’est un code qui n’a pas suivi les évolutions de framework et/ou de langage. Avec les changements de versions, il est devenu difficile d’ajouter une feature et les développeurs passent leur temps à maintenir le code à flot.

-->

---
name: Symptômes d'un code legacy
transition: slide-left
layout: two-cols
class: h-10 opacity-80
---

# Symptômes d’un code legacy
> Comprendre les sources des problèmes

<!-- 

Évolution du modèle (économique, processus, règles)
  ex: Changements réglementaires
>> users que prévu, donc “Mon app ne tient pas la charge”
Perte de maîtrise (connaissance / 1 personne, 0 tests, ..)
Maintenance coûteuse (dette)

 
-->

<div v-click="1" class="flex flex-col justify-center h-full pt-42">
  <h3 class="text-xl font-bold mb-4">🧭 Facteurs externes</h3>
  <ul v-click="2" class="list-disc list-inside space-y-2 text-left">
    <li>Évolution du modèle </li>
    <li>Changements réglementaires</li>
    <li>Turn-over</li>
    <li class="opacity-50">>> users que prévu</li>
    <li class="opacity-50">Pression business pour livrer vite</li>
    <li class="opacity-50">Empilement de demandes clients</li>
    </ul>
</div>

::right::

<div v-click=3 class="flex flex-col pt-40">
  <h3 class="text-xl font-bold mb-4">🔧 Facteurs internes</h3>
  <ul v-click="4"class="list-disc list-inside space-y-2 text-left">
    <li>Vélocité basse <!-- ou ne fait que baisser / + de temps pour amener des new features --></li>
    <li>Bugs et regressions <!-- (fonctionnelles) --></li>
    <li>Connaissance / 1 personne <!-- (!! si ils partent compliqué entreprise de subsister) --></li>
    <li>Couplage fort entre modules</li>
    <li>Absence ou faible couverture de tests</li>
    <li>Manque de documentation</li>
  </ul>
</div>

<!-- Code legacy = coûts + risques -->

---
transition: slide-left
layout: default
class: text-2xl opacity-80
---

# Problèmes pour les devs

<div class="text-xl p-2">

  😤 Rechignement <!-- (olala ça touche à la partie de codebase que j’aime pas). -->
  <br><br>

  ⚡ Tensions <!-- = shipper à la boure (incompréhensions entre les équipes produits et dev. -->
  <br><br>

  😞 Résignation <!-- de tte facon tout le monde s’en fout, la codebase est pourrie, donc je continue à shipper du code pourri. et si ça me saoule un jour je m’en vais. -->
  <br><br>

</div>

---
transition: slide-left
layout: default
class: text-2xl opacity-80
---

# Problèmes pour les entreprises

<div class="text-xl p-2">

  🏃‍♂️ Perte de compétitivité  
  <br><br>
  🚌 “Bus factor”
  <br><br>

</div>

<!--
  Perte compétitivité: Code legacy != que un pb pour les dev, c(‘est un pb  pour l’entreprise !! (ex: si les concurrents sont plus stables, …)

  "Bus Factor": le guru s(en va de l’entreprise (risque stratégique) = plus personne peut maintenir le code existant. Comment faire ???
-->

---
name: Remediation possibles
transition: slide-left
class: opacity-80
---

# 🚨 Situations fréquentes vs 💡 Solutions

<div class="pt-10">
<table class="w-full text-sm border-collapse">
  <thead>
    <tr class="border-b">
      <th class="text-left p-2">🧩 <strong>Situation</strong></th>
      <th class="text-left p-2">🛠️ <strong>Solution</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr v-click="1" class="border-b align-top">
      <td class="p-2">
        <strong>Pas le temps / pas le budget</strong><br>
        <span class="text-gray-500 italic">Perte de maîtrise: risques vs coûts<br>Incompréhension du code</span>
      </td>
      <td class="p-2">
        👉 Présenter les <strong>risques concrets</strong> et les <strong>coûts potentiels</strong>
      </td>
    </tr>
    <tr v-click="2" class="border-b align-top">
      <td class="p-2">
        <strong>Refonte en sous-marin</strong><br>
        <span class="text-gray-500 italic">Estimation faussée volontairement<br>Confiance rompue entre devs et produit.</span>
      </td>
      <td class="p-2">
        🤝 Recréer la <strong>confiance</strong> entre les équipes.
      </td>
    </tr>
    <tr v-click="3" class="align-top">
      <td class="p-2">
        <strong>Refonte sans fin</strong><br>
        <span class="text-gray-500 italic">Deux codebases à maintenir. La nouvelle devient aussi legacy.<br>Aucun plan clair.</span>
      </td>
      <td class="p-2">
        🧭 Besoin de <strong>planification</strong> claire<br>
        📚 <strong>Former</strong> au refacto
      </td>
    </tr>
  </tbody>
</table>
</div>

<!--
  Pas le temps / budget:
    - Souvent lié à une peur de toucher une zone mal comprise du code.
    - La personne n’a pas la maîtrise des risques / coûts réels
  Refonte sous-marin
    -pb de confiance (ex de surestimation de ticket)
    - 🧩 *TODO: Activités d’alignement, ateliers à définir* |
  Refonte sans fin
    - ex: daily.
-->

---
name: Etude de cas banque en ligne qui veut s'etendre à linternational
transition: slide-left
class: opacity-80
---

# Etude de cas

<div class="pt-20 flex flex-col justify-center w-150">
  <Card>
  
  <span v-click>🌎 Banque en ligne française qui veut s'ouvrir à l'international</span>
  <br>

  <span v-click>👛 Besoin: gestion multidevises</span>
  <br>

  <span v-click>🔧 Code <!-- devenu --> complexe et fragile</span>
  <br>
  
  <span v-click>💥 Compréhension difficile</span> <!-- Equipes ont peur de "casser" le "code" ! -->

  </Card>
</div>

<!-- Comment faire ? -->

---
transition: slide-left
layout: two-cols
class: opacity-80
---

# **Mesurer** les risques et les coûts

<!-- TODO: Lire pour la def de la dette; https://www.bitegarden.com/how-to-evaluate-technical-debt-sonarqube -->

<div class="space-y-4">
  <div v-click="1">🧼 <strong>Qualité</strong> de code <span class="opacity-60 text-sm"> (dette, code smells, WTF par minute)</span></div>
  <div v-click="3">🐛 Nombre de <strong>régressions</strong> fonctionnelles</div>
  <div v-click="4">⏱️ Temps <strong>estimé</strong> vs Temps <strong>réel</strong></div>
  <div v-click="5">💸 <strong>Coût réel</strong> par feature</div>
</div>

<!-- 
  Qualité de code: Sonar, ... Par où commencer ?
  Nombre de régressions fonctionnelles: 
  Compter le temps réel passé à faire des correctifs
    => cout réel: "comparer annoncé au po VS pris en vrai pour shipper la feature + corriger pb amenés"
-->

::right::

<div v-click="2" class="flex flex-col justify-center items-center w-full h-full pl-12">
  <img src="/sonarqube-tech-debt.png" />
</div>

<!-- 
Comparer “annoncé au PO” VS “temps réel pris pour shipper la feature + corriger les pb/bugs que ça a amené.”
Une fois qu’on a fait ça, on peut réfléchir à un plan

Note: y'a pas de recette magique qui fonctionne à 100% à chaque fois ! car on fait beaucoup d'humain, et l'humain est faillible: nous avons nos qualités / défaut -> et c'est ça qui rend notre métier passionnant !  
-->

---
transition: slide-left
class: opacity-80
---

# **Proposer** un plan

<h3 v-click>🎯 Périmètre d'intervention</h3>
<br>
<div class="space-y- pl-4">
  <div v-click>🗺️ Définir un périmètre d'<strong>intervention initial</strong></div>
</div>

<br>
  
  <!--
  là ou ça a le plus d'impact ? 
  (on ne refacto pas toute une codebase comme ça d’un coup., mais partie par partie, progressivement. (Exemple: On focus sur la “prise de commande)
  -->

<h3 v-click>🎯 Actions</h3>
<br>
<div class="space-y- pl-4 flex flex-col gap-4">
  <div v-click>🛡️ Pratiques de développement</div>
  <div v-click>🔍 Expliciter les concepts métier</div>
  <span v-click class="text-sm text-gray-500 pl-8">Ex : une colonne "montant" → en fait un montant en euros : migration, renommage, typage</span>
  <div v-click>🚫 Eviter le "code freeze" !</div> <!-- on continue d'intégrer ! -->
  <span v-click class="text-sm text-gray-500 pl-8">Ne pas isoler la refonte sur une branche morte.  
  Indicateur : mesure de la part de "nouveau" code réellement exécuté</span>
</div>

<!-- TODO: put items correctly
### Actions
- Prévenir les anomalies /bugs: utiliser des Value Objects (DDD). PK ?!
- Explicitation (devises/???utiliser exemple) == migration de BDD. (ex: ce montant est un montant en euros)
- Pas de code freeze !: pas partir sur une branche à part et partir du principe que tout s’arrête à côté. Comment ? Indicateur: mesurer la proportion entre le vieux code et le nouveau code qui s’execute.

**COMPARER le coût: refonte VS statut quo**

Tout ça ? => Calculer le cop^put de la refonte (estimation gros grain à ce stade)(en nombre de jour à investir
	Comparer coût refonte VS statut quo(=si on change rien)

Une fois qu’on a ces deux coûts ? 

A quoi nous revient la refonte (commencer à estimer le nb de jours à investir vs si on change rien)
 -->

---
transition: slide-left
class: opacity-80
---

# 🤝 **Communiquer** avec les parties prenantes

> Se synchroniser et avancer collectivement

<br>

<div class="space-y-4">
  <div v-click>📣 Informer</div>
  <!-- <span class="text-sm text-gray-500 italic">
  Les personnes impactées par notre refonte des coûts et risques actuels (ex: équipe produit, devises)
  </span> -->
  <div v-click>🗺️ Présenter le plan de <strong>refonte</strong></div>
  <!-- <span class="text-sm text-gray-500 italic">
  Montrer en quoi la refonte répond aux problèmes identifiés
  </span> -->
  <div v-click>🤝 <strong>Négocier</strong> la planification</div>
  <!-- <span class="text-sm text-gray-500 italic">
  Avec le PO ou les sponsors : diplomatie et intelligence collective
  </span> -->
  <div v-click>✅ Obtenir l’<strong>accord</strong> de la direction</div>
  <!-- <span class="text-sm text-gray-500 italic">
  Discussion avec les décideurs (CTO, VP Engineering…)
  </span> -->
  <div v-click>🎯 Aligner avec la <strong>stratégie d’entreprise</strong></div>
  <!-- <span class="text-sm text-gray-500 italic">
  Montrer l'alignement entre la refonte et les objectifs globaux
  </span> -->
</div>

<!--
  parties prenantes <=> collègues
  notes...
-->

---
transition: slide-left
class: opacity-80
--- 

# 👁️‍🗨️ **Suivre** et donner de la **visibilité**

  <br>

  <span v-click>🚧 Éviter l’**effet tunnel**</span> <!-- <span class="text-sm text-gray-500">Comment ? PoC, baby steps (Mikado), déploiements réguliers</span> -->
  <br>

  <span v-click>⏪ Tout changement est rollback-able rapidement</span> <!-- == sécurité -->
  <br>

  <span v-click> 📢 **Partager l'avancement** → feedback</span> <!-- Permet de négocier : qualité, ajustements, arbitrages justifiés -->
  <br>

<!-- 
Une fois qu’on rentre dans la phase de refonte, il faut faire un suivi, et rassurer les gens avec qui on va travailler.
!! risque que ça pète est gros,
!! commencer par tacler les projets les + ambitieux en 1er 
	!! sur les tous petits périmètres… pour voir si l’approche fonctionne ou pas (PöC

éviter l’effet tunnel: …POC, baby steps + déploiements réguliers (ça spasse pas bien, on connait la cause !,

Vérifier qu’on peut annuler un changement (=rollback) < 1 min (très rapidement, TODO: vérifier le time !)
Mettre en place des indicateurs qui ne peuvent pas régresser: CI, warnings, …
Le but de tout çà ?
Partager l’avancement avec les personnes intéressées
ET négocier des ajustements si nécessaire (ex: coordination des diffferentes taches avec les equipes produits (TODO: prendre un exemple)
!! Etre transparent syr les risques (tenir au courant les personnes impactées) !! 

-->

---
transition: slide-left
layout: center
class: opacity-80
---

<Card>
<!-- {theme: 'neutral', scale: 0.5} -->
```mermaid {scale: 1.0}
graph TD
A[Mesurer les risques / coûts] --> B
B[Proposer un plan] --> C
C[Communiquer] --> D
D[Suivre & Rassurer]
```
</Card>

<!-- TODO: peutêtre surligner par étape pour la lisibilité !! (solution: ressortir ce diagramme à chaque étape) -->

---
transition: slide-up
layout: statement
class: text-4xl
---

❝ Legacy code is about the **cost of change** ❞

<span class="text-base text-gray-500">— Michael Feathers</span>

<!-- ... -->

<style>
strong {
  color: #2B90B6;
}
</style>

---
name: Réécriture ou travailler avec lexistant (Brownfield)
transition: slide-left
layout: image
image: https://images.unsplash.com/photo-1748701821466-0b9f8bf839ac?q=80&w=2051&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
class: text-xl flex flex-col justify-center opacity-80
---

# Un peu de réécriture

<Card class="w-134 mt-10">

### **Brownfield** development

🐌 Reprise de l’existant
<br><br>
💸 Surprises dans le legacy
<br><br>
🔐 Stack de l’existant
<br><br>
🔥 Risques d’endettement ++ (bugs, dette, deps.)
<br><br>
🧩Challenge: Intégrer des nouvelles features
</Card>

<style>
h3 {
  color: #2B90B6;
}
</style>

<!-- notes.. -->

---
name: Réécriture from scratch (Greenfield)
transition: slide-left
layout: image
image: https://images.unsplash.com/photo-1506260408121-e353d10b87c7?q=80&w=2128&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
class: text-xl flex flex-col justify-center opacity-80
---

# Un peu de réécriture

<Card class="w-134 mt-10">

### **Greenfield** development


⏳Délai initial plus court
<br><br>
💰 Budget prévisible
<br><br>
🧱 Stack technique / architecture: choix libre
<br><br>
🟢 Peu de risques / complexité (0 dette)
<br><br>
🧩 Nécessite décisions: UI, backend, infra, tests…
</Card>

<style>
h3 {
  color: #2B90B6;
}
</style>

<!-- notes.. -->

---
transition: slide-left
layout: image
image: brownfield.png
---

# Prendre une décision

<Card>

  <div v-click>
    <h4>🚀 Réécrire</h4>
    <i class="opacity-60">
      <div>“ Le code existant est un handicap (pas de tests, pas de documentation, mauvaise structure) ”</div>
      <div>“ Vous disposez du temps, du budget et de la tolérance au risque nécessaires pour le reconstruire ”</div>
    </i>
    <br>
  </div>

  <div v-click>
    <h4>🏗️ Rearchitect</h4>
    <i class="opacity-60">
      <div>“ L'architecture de votre système limite la croissance ”</div>
      <div>“ Vous passez à des services en microservices ”</div>
    </i>
    <br>
  </div>

  <div v-click>
    <h4>🔧 Refactor</h4>
    <i class="opacity-60">
      <div>“ Vous pouvez nettoyer le code en toute sécurité et de manière incrémentale,</div>
      <div>sans trop impacter les fonctionnalités existantes ”</div>
   </i>
    <br>
  </div>
</Card>

<!-- notes.. -->

---
transition: slide-up
layout: statement
class: text-4xl
---

❝ On choisit de s'orienter vers

un **refactoring progressif** ❞

<style>
strong {
  color: #2B90B6;
}
</style>

<!-- ... -->

---
transition: slide-left
layout: center
---

# Réarchitecturer

Strangling the monolith

<img src="/strangling-the-monolith.png" class="w-95" />

<!--
  Rearchitecturer = Modifier la structure du code (parfois en changeant le comportement de l'application)
 -->

---
transition: slide-left
layout: center
---

# Réarchitecturer

Branch-by-abstraction

<img src="/branch-by-abstraction.png" class="h-60" />

<!-- notes.. -->

---
transition: slide-left
---

<!-- Slide noire de transition -->

---
name: Notre exemple de refacto le Trivia
transition: slide-left
layout: image-right
image: /trivia-game.jpg
class: opacity-80
---

# Notre exemple
Jeu du Trivia

  <span v-click>🚀 Jeu de questions réponses</span>
  <br>

  <span v-click>🔧 Code <!-- devenu --> complexe et fragile</span>
  <br>
  
  <span v-click>💥 Compréhension difficile</span> <!-- Equipes ont peur de "casser" le "code" ! -->
  <br><br>

<!-- Comment faire ? -->

<style>
strong {
  color: #2B90B6;
}
</style>

---
name: Refactorer code legacy focus on business value
transition: slide-left
layout: image
image: https://images.unsplash.com/photo-1634207284450-f6ad4451b94f?q=80&w=880&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# class: text-xl flex flex-col justify-center
class: opacity-80
---

# Refactorer dans du code legacy

Recette étape par étape

<Card class="card w-134 mt-10 text-xl">

🔦 Identifier les hotspots <!-- seams: fakeDB, seam object, 3rd party server, -->
<br><br>
🔨 Casser les dépendances
<br><br>
🧪 Ecrire les tests <!-- nécessaires (UT, definition: <100ms and 1 feature) -->
<br><br>
🔧 Effectuer un changement
<br><br>
🧩 Refactorer <!-- si besoin -->
</Card>

<style>
h3 {
  color: #2B90B6;
}
p {
  color: #012;
}

.card p {
  color: unset;
}
</style>

<!-- notes.. -->

---
name: Refactoring example Identifier les hotspots
transition: slide-left
class: opacity-80
---

# Identifier les hotspots

> Quand ? vous ne savez pas par où commencer, votre temps est limité --> ROI

<!-- Besoin: Pas un truc parfait, mais d'un Indicateur qui vous => prendre des décisions plutôt que faire des hypothèses (CodeClimate) -->

<h3>Comment ?</h3>
  1. Calculer la Complexité du Code (fichiers SonarQube) <!-- TODO: regarder  --> <!-- code-complexity (node), base sur num LoC -->
  <br><br>
  2. Calculez le Churn <!-- frequence de modification -->

  ```ts {*}
    git log --format=format: --name-only --since=12.month \
    | egrep -v '^$' \
    | egrep -v '\\.json$' \
    | sort \
    | uniq -c \
    | sort -nr \
    | head -50
  ```

  <!-- nécessaires (UT, definition: <100ms and 1 feature) -->

  <br>
  3. Meilleur ROI = Complexité <span class="opacity-60 text-xs">(Important)</span> * Churn <span class="opacity-60 text-xs">(Urgent)</span>
  <span class="opacity-60 text-xs pl-4">Augmente votre vélocité</span>
  <br>

<!-- 
1.
2.
  git log: récupère des logs
  egrep: retire toutes les lignes vides
  sort: tri alpha
  uniq -c: compte les occurences de chaque nom de fichier
  sort -nr: trie résultats, décroissant
  head -50: garde 50 noms de fichiers les plus changés
3.
 -->

---
name: Refactorer code legacy | Focus on business value
transition: slide-left
#layout: image
#image: https://images.unsplash.com/photo-1576153192396-180ecef2a715?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
class: opacity-80
---

# Refactorer dans du code legacy

Focus sur la **valeur** métier

<Card class="flex flex-row w-160">
  <img src="/refactoring-most-valued-features.png" />
</Card>

<!-- notes.. -->

---
name: Refactoring example Identifier les hotspots
transition: slide-left
class: opacity-80
---

# Identifier les hotspots

> Quand ? vérifier les impacts d'un changement

  <br>
  <h3>Diagramme de dépendance</h3>
  
  <img src="/dependency-diagram-petclinic.png" alt="dependency diagram petclinic" />

<!-- 
  ...
 -->
 
  <!-- Mikado = graphe de dépendance; libère charge mentale; partage avec pairs -->
  <!-- compléter objectifs par les bords du graph == safe ! => livrer en plusieurs fois -->

---
name: Refactoring example Identifier les hotspots
transition: slide-left
class: opacity-80
---

# Identifier les hotspots

> Quand ? vérifier les impacts d'un changement

  <br>
  <h3>Matrice de dépendance</h3>
  
  <img src="/dependency-matrix-petclinic.png" alt="dependency matrix petclinic" />

---
name: Refactorer code legacy | Scratch Refactoring et Exploratoire
transition: slide-left
#layout: image
#image: https://images.unsplash.com/photo-1576153192396-180ecef2a715?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
---

# Découvrir du code legacy

Scratch Refactoring + Refactoring Exploratoire

> Quand ? Vous essayez de comprendre ce que le code fait vraiment

<br>

> Pratique >> Analyse théorique

<br>

<Card class="flex flex-row w-160">
  <img src="/scratch-refacto-timer.png" />
</Card>

<br>

> Permet ? Big Picture

<!--
Refacto Exploratoire

> quand ? avant les refactos structurels (Extract Function)
"Ce qui change en meme temps devrait être gardé à proximité"
!! risqué si pas de tests.
-->

<!--
  Conseils d'uilisation de refacto (auto)
  + attention aux break;continue;return;
  +
    1. Extraire toutes les magic strings et les magic numbers
    2. Extraire des bouts de code dans des fonctions
    3. Inline ces fonctions à nouveau
 -->

---
name: Scratch refacto | Ce qu'on a appris.
transition: slide-left
layout: image-right
image: /trivia-game.jpg
---

# Scratch Refactoring

Ce qu'on a appris

- Deux points d'entrée 'public': add() et roll()

- add(): initialize player data + affichage

- roll(): determine si le joueur est piégé ou non ET le déplace


---
transition: slide-left
layout: statement
class: text-4xl opacity-80
---

# Tester

<style>
h1, h2 {
  color: #2B90B6;
}
</style>

---
name: Refactorer code legacy | Approval tests
transition: slide-left
---

# Approval Tests <!-- Golden, Characterization, Snapshot(React) -->

> Quand ? Mon code n'a aucun tests, je ne sais pas ce qu'il fait.

E2E >= Approval Tests >= Unit Test

https://approvaltests.com/

<div class="flex items-center justify-center gap-20">

  <img v-click="1" src="/approval-tests-boite-noire.png" class="h-20" />

  <!-- Left: Received -->
  <div v-click="2" class="flex flex-col items-center">
    <div class="text-7xl">📄</div>
    <div class="mt-2 text-xl font-medium text-gray-400">File Received</div>
  </div>

  <!-- Arrow -->
  <div v-click="3" class="text-5xl text-gray-400">➡️</div>

  <!-- Right: Approved -->
  <div v-click="4" v-mark="4" class="flex flex-col items-center">
    <div class="text-7xl">📄</div>
    <div class="mt-2 text-xl font-medium text-green-700">File Approved</div>
  </div>

</div>

<!--
  [Démo] Générer tests chara (créer un test 'add player')
  [Démo][add()] simuler un changement (commenter un console.log)
  Vérifier la nouvelle couverture de test:
    - IntelliJ/Sonar
    - PiTest (mutation testing), [opt] vérifier le N fois execution au niveau de la ligne ;)
  [Démo][add()] Commenter player.push() -> tests vont fail (boucle infinie)
  corriger
  commenter ligne d'en dessous -> fail
  [Démo] Générer test 'add player roll' (avec un roll à 777)

  [Démo][add()][opt] Ajouter un param/méthode/log pour 'tracker' les états des variables privées (ex: places)

-->

---
transition: slide-up
layout: statement
class: text-4xl opacity-80
---

❝ je dois **tester** avant de refacto,
<br>
<br>

mais mon code est **intestable** ❞

<!-- ... -->

---
name: Refactorer code legacy | Decoupler Core vs Infra
transition: slide-left
layout: statement
class: text-xl
---

## **Découpler** : Core vs Infrastructure

<style>
  strong {
    color: #2B90B6;
  }
</style>

<!--
Quand ? J'ai un appel db / infra en plein milieu de mon code

  code infra = dépend de système externe, besoin d'un environnement pour s'executer (ex:db, I/O System(logs))
  code core (domaine) = logique pure, depend de rien

  ex: dans notre exemple, console.log et math.random
-->

---
name: Refactorer code legacy | Subclass & Override
transition: slide-left
layout: default
class: 
---

# Subclass & Override

> Quand ? le code existant (non testé) a des effets de bords empêchant d'écrire des tests (appels BDD, ...).

<br>

> Solution: extraire l'infrastructure (ex: logs, appels BDD) dans des méthodes dédiées.

<br>

````md magic-move {lines: true}
```ts {*|1,9,10}
// Before Subclass & Override
public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    System.out.println(playerName + " was added");
    System.out.println("They are player number " + players.size());

    return true;
  }

```
```ts {1,9-10}
// 1. Extract Variable sur le premier argument du println
public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    String message = playerName + " was added";
    System.out.println(message);
    System.out.println("They are player number " + players.size());
    
    return true;
  }
```
```ts {1,10,14-17}
// 2. Extract Method sur le premier println
public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    String message = playerName + " was added";
    log(message)
    System.out.println("They are player number " + players.size());
    
    return true;
  }

private void log(String message) {
  System.out.println(message);
}
```
```ts {1,9}
// 3. Inline variable sur la variable message
public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    log(playerName + " was added");
    System.out.println("They are player number " + players.size());
    
    return true;
  }

private void log(String message) {
  System.out.println(message);
}
```
```ts {1,10}
// 4. Refactoring manuel (ok car on peut 'rollback' avec un Inline Method sur la méthode modifiée)
public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    log(playerName + " was added");
    log("They are player number " + players.size());
    
    return true;
  }

private void log(String message) {
  System.out.println(message);
}
```
```ts {1,14-17}
// 5. On expose log() en protected pour les tests
public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    log(playerName + " was added");
    log("They are player number " + players.size());

    return true;
  }

  protected void log(String message) {
    System.out.println(message);
  }
```
```ts {*|3-5}
// 6. Subclass Game pour les tests
class TestableGame extends Game {
  protected log(message: string): void {
    /* Override: doing nothing.. */
  }
}
```
````

<span v-click>

<br>

>Seam : endroit où on peut rajouter un morceau de code sans modifier le code existant
<!-- => Casser les dépendances ! -->
<!-- va nous => modifier le comportement du code dans les tests -> pouvoir tester le reste du code -->

</span>

<!-- 
  Subclass & Override: aide à détecter les morceaux d'infrastructure afin de pouvoir écrire les tests manquants

  > Avantage de cette technique ? Si on change de stratégie de log, on ne change pas les tests
  -> tests découplés de la stratégie de log :D
  Si vous faites l'inverse, les tests vont "solidifier" les choix d'implem. -> besoin de tout changer après.
-->

---
name: Refactorer code legacy | Move Function to Delegate
transition: slide-left
---

# Move Function to Delegate

> Quand ? Après Subclass & Override. Améliorer le design du code à partir des tests.

<!-- TODO [opt]: si tu as le temps, coordoner le shiki magic move between left(Game class) and right (interface/implem) -->

````md magic-move {lines: true}
```ts {*|14-21}
class Game {
  public boolean add(String playerName) {

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    log(playerName + " was added");
    log("They are player number " + players.size());

    return true;
  }

  protected void log(String message) {
    System.out.println(message);
  }

  class TestableGame extends Game {
    protected log(String message): void {
      /* Override: doing nothing.. */
    }
  }
}
```
```ts {*}
// 1. Créer une interface qu'on aimerait utiliser: Logger
interface Logger {
  void log(String message);
}
```
```ts {*}
// 2. Créer une interface qu'on aimerait utiliser: Logger
interface Logger {
  void log(String message);
}

class ConsoleLogger implements Logger {
  void log(String message) {

  }
}
```
```ts {4|17-19}
// 3. Move Method (ou Move Function) refactoring
class Game {
  public boolean add(String playerName) {
    private Logger logger = new ConsoleLogger();

    players.add(playerName);
    places[howManyPlayers()] = 0;
    purses[howManyPlayers()] = 0;
    inPenaltyBox[howManyPlayers()] = false;

    log(playerName + " was added");
    log("They are player number " + players.size());

    return true;
  }

  protected void log(String message) {
    System.out.println(message);
  }

  class TestableGame extends Game {
    protected log(String message): void {
      /* Override: doing nothing.. */
    }
  }
}
```
```ts {6-9}
// 4. Créer une interface qu'on aimerait utiliser: Logger
interface Logger {
  void log(String message);
}

class ConsoleLogger implements Logger {
  void log(String message) {
    System.out.println(message);
  }
}
```
```ts {*}
// 5. Injecter le 'Logger' Delegate dans le constructeur
class Game {
  public boolean add(String playerName) {
    private Logger logger = new ConsoleLogger();

    // code..
```
```ts {*}
// 5. Injecter le 'Logger' Delegate dans le constructeur
class Game {
  public boolean add(String playerName) {
  public Game(Logger logger) {
    logger = new ConsoleLogger();
  }
  // code..
```
```ts {*}
// 4. Créer une interface qu'on aimerait utiliser: Logger
interface Logger {
  void log(String message);
}

class ConsoleLogger implements Logger {
  void log(String message) {
    System.out.println(message);
  }
}
```
```ts {1,12-16}
// 5. Créer une implémentation dédiée à nos tests pour Logger
interface Logger {
  void log(String message);
}

class ConsoleLogger implements Logger {
  void log(String message) {
    System.out.println(message);
  }
}

// Pour les tests
class NoopLogger implements Logger {
  void log(String message) { /* NoOp = ne fait rien */ }
}
```
```ts {*}
class TestableGame extends Game {
  protected log(String message): void {
    /* Override: doing nothing.. */
  }
}
```
```ts {*}
class TestableGame extends Game {
  public TestableGame() {
    super(new NoopLogger()); // Laisse l'instance de logger gérer le comportement
  }
}
```
````

<!--
  Etape 3. Si on utilise l'inversion de dépendance avec Spring -> directement injecter dans le constructeur
-->

---
name: TMP conseils refacto dans codebase legacy
transition: slide-left
---

# Refactorer dans du code legacy

A retenir

<h3 v-click>Stratégie non prédictive</h3> <!-- complexité masquée (ex et tu vas le découvrir.. comment ?) -->
  <ul>
    <li v-click>Fail-fast</li>
    <li v-click>Scratch refactoring et exploratoire</li>
    <li v-click>Test-first</li>    
    <li v-click>Méthode Mikado</li>
    <!--
      stratégie de refacto
      on part sur une strat avec un but,
      on continue jusqu'à ou on perd le controle
      quand ça pete, on revient en arrière,
      on change de direction (.. ex: on peut pas faire X -> tests approvals)
    -->
    <li v-click>Over-committing (minuteur: N minutes) ou git add -p</li> <!-- But: capable de travailler rapidement et de façon sécuritaire sur n'importe quel code -->
  </ul>
  <br>
<h3 v-click>Besoin d'un filet de sécurité efficace</h3>
  <ul>
    <li v-click>Approval testing</li> <!-- car si y'a pas de test -> on peut rien faire -->
    <!--
      📸 Génère un texte que tu peux capturer
      ✅ Utilise la couverture de tests pour trouver toutes les combinaisons à tester
      👽 Introduit des mutations pour vérifier la qualité de test tests
    -->
    <li v-click>Mutation testing</li> <!-- vérifier la pertinence des tests -->
  </ul>
  <!--
  <h3>Reduire la charge cognitive (on se perd, on se rappelle plus du code après N time, ...)</h3>
  <ul>
  <li>clean code</li>
  <li>typage</li>
  </ul>
  -->

<style>
h3 {
  color: #2B90B6;
  font-size: 18pt;
}
h3 div {
  padding: 8px;
}
ul {
  padding-left: 20pt;
}
</style>

<!-- notes -->

---
transition: slide-up
layout: cover
background: https://images.unsplash.com/photo-1572883454114-1cf0031ede2a?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
---

## Conclusion

<div class="absolute bottom-10 right-60 w-50 flex flex-row items-center">
````md magic-move {lines:false}
```ts {*}
  doStuff()
```
```ts {*}
  handleData()
```
```ts {*}
  processConference()
```
```ts {*}
  attendTechConference()
```
```ts {*}
  attendVoxxedDaysToLearn()
```
```ts {*}
  attendVoxxedDays2025ToStayUpdatedOnJava()
```
```ts {*}
  enjoyVoxxedDaysLuxembourg2025ForArchitectureAndDevTrends()
```
````
</div>

<style>
h2 {
  font-size: 28pt;
  opacity: 0.8
}
</style>

---
transition: slide-up
layout: image
image: /slide-quelques-references.png
---

# Quelques références

<style>
h1 {
  color: #2B90B6;
}
</style>

---
layout: image
image: /slide-outro.png
---

---
transition: slide-left
---

<!-- Slide noire de transition -->

---
transition: slide-up
level: 2
---

# Navigation

Hover on the bottom-left corner to see the navigation's controls panel, [learn more](https://sli.dev/guide/ui#navigation-bar)

## Keyboard Shortcuts

|                                                     |                             |
| --------------------------------------------------- | --------------------------- |
| <kbd>right</kbd> / <kbd>space</kbd>                 | next animation or slide     |
| <kbd>left</kbd>  / <kbd>shift</kbd><kbd>space</kbd> | previous animation or slide |
| <kbd>up</kbd>                                       | previous slide              |
| <kbd>down</kbd>                                     | next slide                  |

<!-- https://sli.dev/guide/animations.html#click-animation -->
<img
  v-click
  class="absolute -bottom-9 -left-7 w-80 opacity-50"
  src="https://sli.dev/assets/arrow-bottom-left.svg"
  alt=""
/>
<p v-after class="absolute bottom-23 left-45 opacity-30 transform -rotate-10">Here!</p>

---
layout: two-cols
layoutClass: gap-16
---

# Table of contents

You can use the `Toc` component to generate a table of contents for your slides:

```html
<Toc minDepth="1" maxDepth="1" />
```

The title will be inferred from your slide content, or you can override it with `title` and `level` in your frontmatter.

::right::

<Toc text-sm minDepth="1" maxDepth="2" />

---
layout: image-right
image: https://cover.sli.dev
---

# Code

Use code snippets and get the highlighting directly, and even types hover!

```ts [filename-example.ts] {all|4|6|6-7|9|all} twoslash
// TwoSlash enables TypeScript hover information
// and errors in markdown code blocks
// More at https://shiki.style/packages/twoslash
import { computed, ref } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)

doubled.value = 2
```

<arrow v-click="[4, 5]" x1="350" y1="310" x2="195" y2="342" color="#953" width="2" arrowSize="1" />

<!-- This allow you to embed external code blocks -->
<<< @/snippets/external.ts#snippet

<!-- Footer -->

[Learn more](https://sli.dev/features/line-highlighting)

<!-- Inline style -->
<style>
.footnotes-sep {
  @apply mt-5 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

<!--
Notes can also sync with clicks

[click] This will be highlighted after the first click

[click] Highlighted with `count = ref(0)`

[click:3] Last click (skip two clicks)
-->

---
level: 2
---

# Shiki Magic Move

Powered by [shiki-magic-move](https://shiki-magic-move.netlify.app/), Slidev supports animations across multiple code snippets.

Add multiple code blocks and wrap them with <code>````md magic-move</code> (four backticks) to enable the magic move. For example:

````md magic-move {lines: true}
```ts {*|2|*}
// step 1
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})
```

```ts {*|1-2|3-4|3-4,8}
// step 2
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
}
```

```ts
// step 3
export default {
  data: () => ({
    author: {
      name: 'John Doe',
      books: [
        'Vue 2 - Advanced Guide',
        'Vue 3 - Basic Guide',
        'Vue 4 - The Mystery'
      ]
    }
  })
}
```

Non-code blocks are ignored.

```vue
<!-- step 4 -->
<script setup>
const author = {
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
}
</script>
```
````

---

# Components

<div grid="~ cols-2 gap-4">
<div>

You can use Vue components directly inside your slides.

We have provided a few built-in components like `<Tweet/>` and `<Youtube/>` that you can use directly. And adding your custom components is also super easy.

```html
<Counter :count="10" />
```

<!-- ./components/Counter.vue -->
<Counter :count="10" m="t-4" />

Check out [the guides](https://sli.dev/builtin/components.html) for more.

</div>
<div>

```html
<Tweet id="1390115482657726468" />
```

<Tweet id="1390115482657726468" scale="0.65" />

</div>
</div>

<!--
Presenter note with **bold**, *italic*, and ~~striked~~ text.

Also, HTML elements are valid:
<div class="flex w-full">
  <span style="flex-grow: 1;">Left content</span>
  <span>Right content</span>
</div>
-->

---

# Clicks Animations

You can add `v-click` to elements to add a click animation.

<div v-click>

This shows up when you click the slide:

```html
<div v-click>This shows up when you click the slide.</div>
```

</div>

<br>

<v-click>

The <span v-mark.red="3"><code>v-mark</code> directive</span>
also allows you to add
<span v-mark.circle.orange="4">inline marks</span>
, powered by [Rough Notation](https://roughnotation.com/):

```html
<span v-mark.underline.orange>inline markers</span>
```

</v-click>

<div mt-20 v-click>

[Learn more](https://sli.dev/guide/animations#click-animation)

</div>

---

# Diagrams

You can create diagrams / graphs from textual descriptions, directly in your Markdown.

<div class="grid grid-cols-4 gap-5 pt-4 -mb-6">

```mermaid {scale: 0.5, alt: 'A simple sequence diagram'}
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

```plantuml {scale: 0.7}
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}

database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}

[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```

</div>

Learn more: [Mermaid Diagrams](https://sli.dev/features/mermaid) and [PlantUML Diagrams](https://sli.dev/features/plantuml)

---
src: ./pages/imported-slides.md
hide: false
---

---

# Monaco Editor

Slidev provides built-in Monaco Editor support.

Add `{monaco}` to the code block to turn it into an editor:

```ts {monaco}
import { ref } from 'vue'
import { emptyArray } from './external'

const arr = ref(emptyArray(10))
```

Use `{monaco-run}` to create an editor that can execute the code directly in the slide:

```ts {monaco-run}
import { version } from 'vue'
import { emptyArray, sayHello } from './external'

sayHello()
console.log(`vue ${version}`)
console.log(emptyArray<number>(10).reduce(fib => [...fib, fib.at(-1)! + fib.at(-2)!], [1, 1]))
```

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/resources/showcases)

<PoweredBySlidev mt-10 />
