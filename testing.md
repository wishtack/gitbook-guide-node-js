# Testing

L'unit-testing n'est pas optionnel.

Avec un langage dynamiquement typé comme le JavaScript, si la couverture de code par les tests n'est pas suffisante, nous ne sommes même pas à l'abris des erreurs de syntaxe.

{% hint style="warning" %}
Pas de tests unitaires  
=&gt; pas de refactoring & pas d'update de dépendances  
=&gt; dette technique & régression perpétuelle  
=&gt; peur du changement  
=&gt; vélocité 0
{% endhint %}

{% hint style="info" %}
Les tests unitaires permettent de localiser immédiatement les sources des erreurs.
{% endhint %}

**Les tests unitaires doivent être implémentés en premier.**

[https://guide-agile.wishtack.io/extreme-programming/testing](https://guide-agile.wishtack.io/extreme-programming/testing)

{% embed data="{\"url\":\"https://guide-agile.wishtack.io/extreme-programming/testing\",\"type\":\"link\",\"title\":\"Testing - Le Guide Agile par Wishtack\",\"icon\":{\"type\":\"icon\",\"url\":\"https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/spaces%2F-LHD4wSD1i9v5yCa767m%2Favatar.png?generation=1531392281890174&alt=media\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.gitbook.com/share/space/thumbnail/-LHD4wSD1i9v5yCa767m.png\",\"width\":1200,\"height\":630,\"aspectRatio\":0.525}}" %}

La modularité facilite l'implémentation des tests unitaires.

## Les Outils

Il existe plusieurs frameworks et outils pour implémenter les tests unitaires Node.js

Les frameworks les plus utilisés sont Jasmine et Mocha. Ceux-ci étant très similaires, il est recommandé d'utiliser Jasmine qui permet également d'implémenter les tests Angular.

[http://thejsguy.com/2015/01/12/jasmine-vs-mocha-chai-and-sinon.html](http://thejsguy.com/2015/01/12/jasmine-vs-mocha-chai-and-sinon.html)

{% embed data="{\"url\":\"http://thejsguy.com/2015/01/12/jasmine-vs-mocha-chai-and-sinon.html\",\"type\":\"link\",\"title\":\"Jasmine vs. Mocha, Chai, and Sinon - David Tang\",\"description\":\"Thoughts and tutorials on JavaScript, frameworks, testing, and patterns\"}" %}

  
[http://jasmine.github.io/](http://jasmine.github.io/)

{% embed data="{\"url\":\"http://jasmine.github.io/\",\"type\":\"link\",\"title\":\"Jasmine Documentation\",\"icon\":{\"type\":\"icon\",\"url\":\"https://jasmine.github.io/favicon.ico\",\"aspectRatio\":0}}" %}

[https://mochajs.org/](https://mochajs.org/)

{% embed data="{\"url\":\"https://mochajs.org/\",\"type\":\"link\",\"title\":\"Mocha - the fun, simple, flexible JavaScript test framework\",\"icon\":{\"type\":\"icon\",\"url\":\"https://mochajs.org/static/favicon.copy.f17f048f84.ico\",\"aspectRatio\":0}}" %}

[https://jestjs.io/](https://jestjs.io/)

{% embed data="{\"url\":\"https://jestjs.io/\",\"type\":\"link\",\"title\":\"Jest · 🃏 Delightful JavaScript Testing\",\"description\":\"🃏 Delightful JavaScript Testing\",\"icon\":{\"type\":\"icon\",\"url\":\"https://jestjs.io/img/favicon/favicon.ico\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://jestjs.io/img/opengraph.png\",\"width\":796,\"height\":416,\"aspectRatio\":0.5226130653266332}}" %}

