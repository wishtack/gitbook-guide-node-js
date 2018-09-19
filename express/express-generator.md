# Express Generator

{% hint style="info" %}
Vous n'allez bien sûr pas implémenter l'intégralité de l'application en un seul fichier.
{% endhint %}

Pour initialiser la structure du produit, vous pouvez utiliser le module `express-generator` qu'il vaut mieux installer globalement.

```bash
yarn global add express-generator # or: npm install --global express-generator

# Initialize product with Handlebars templating engine, SASS as a css engine and initialize .gitignore file.
express product-name --hbs --css sass --git

# Install node dependencies.
cd product-name && yarn install
```



