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

## Jasmine

### Exemple avec Jasmine

```javascript
const cache = require('cache');
const User = require('user');
const Wish = require('wish');

describe('User', () => {

    beforeEach(() => {
        cache.clear();
    });

    afterEach(() => {
        cache.clear();
    });

    it('should add wishes', function() {

        const user = new User();
        const wish = new Wish({title: 'Holidays'});

        /* Add a wish. */
        user.addWish(wish);

        /* Check wishlist. */
        expect(user.wishList().length).toEqual(1);
        expect(user.wishList()[0].title()).toEqual('Holidays');

    });

});
```

### Exécution des tests avec `jasmine-node`

```javascript
yarn add --dev jasmine-node

yarn jasmine-node --autoTest --watchFolders app.js routes views test/unit
```

### Jasmine's Spies

Les _spies_ de Jasmine sont une implémentation de _mocks_.

Ils permettent d'implémenter des tests comportementaux. Autrement dit, ils permettent de simuler le comportement d'une partie de code que l'on souhaite exclure du test unitare.

Sans _mocks_, les tests seraient des tests d'intégration et non des tests unitaires.

```javascript
describe('SearchEngine', () => {

    it('should pass locale to third party api', () => {

        /* Spying on `thirdPartySearchApi.search` and faking result. */
        spyOn(thirdPartySearchApi, 'search').and.returnValue([
            {
                title: 'Wishtack - Making Your Wishes Come True',
                url: 'https://www.wishtack.com'
            }
        ]);

        /* Trigger search. */
        searchEngine.search({keywords: 'Wishtack'});

        /* Check spy's call count. */
        expect(thirdPartySearchApi.search.callCount).toBe(1);

        /* Check spy's call args. */
        expect(thirdPartySearchApi.search).toHaveBeenCalledWith({
            country: 'US',
            keywords: 'Wishtack',
            language: 'en'
        });

    });

});
```

{% hint style="warning" %}
Pensez à tester les cas d'erreur !
{% endhint %}

## **HTTP Testing**

Pour tester le _routing_ et les interactions avec le serveur, il faut simuler les requêtes à l'aide d'outils comme `supertest`.

**https://github.com/visionmedia/supertest**

{% embed data="{\"url\":\"https://github.com/visionmedia/supertest\",\"type\":\"link\",\"title\":\"visionmedia/supertest\",\"description\":\"Super-agent driven library for testing node.js HTTP servers using a fluent API - visionmedia/supertest\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars3.githubusercontent.com/u/9285252?s=400&v=4\",\"width\":400,\"height\":400,\"aspectRatio\":1}}" %}

```javascript
const express = require('express');
const request = require('supertest');

describe('wishes RESTful API', () => {

    it('should return wishes', (done) => {

        request(app)
            .get('/users/123456/wishes/')
            .set('Accept', 'application/json')
            .expect(200, [
                {
                    id: 'abcdef',
                    title: 'Holidays'
                }
            ], done);

    });
    
});
```

