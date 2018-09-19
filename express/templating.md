# Templating

Express est compatible avec de nombreux moteurs de _templating_ JavaScript.

Express est fourni avec les moteurs suivants : Jade, EJS et Mustache.

## Jade _\(moteur par défaut\)_

Une affaire de goût.

```text
extends layout

block content

    if data
        div.container
            h1= title
            ul
                each person in data
                li= person.name
```

## EJS _\(Embedded JavaScript\)_

Syntaxe ****complexe.

```markup
<%- include head.ejs %>

    <% if(data) { %>
        <div class="container">
            <h1> <%= title %> </h1>
            <ul>
                <% data.forEach(function(person){ %>
                <li title="job: <%= person.job %> status: <%= person.status %>">
                <%= person.name %>
                </li>
                <% }); %>
            </ul>
        </div>
    <% } %>

<%- include foot.ejs %>
```

## JSHTML

```markup
<html>
<head>
    <title>@locals.title</title>
</head>

<body>

<ul class="Task">
@for(var taskIndex = 0, taskCount = locals.taskList.length; taskIndex < taskCount; taskIndex ++){
    var task = locals.taskList[taskIndex];
    <li class="@(taskIndex % 2 ? "Odd" : "Even")">
    <a href="/task/@task.id">@task.name</a>
    </li>
}
</ul>

</body>
</html>
```

## Mustache / Hogan.js.

Pas de précompilation des templates avec _Mustache_.

_Hogan**.**js_ ****implémente ****les mêmes ****fonctionnalités ****que ****_Mustache_ ****avec ****la ****précompilation ****en ****plus.

```markup
{{>head}}

{{#hasData}}
<div>
    <h1> {{title}} </h1>
    <ul>
        {{#data}}
        <li title="job: {{job}} status: {{status}}">
            {{name}}
        </li>
        {{/data}}
    </ul>
</div>
{{/hasData}}

{{>foot}}
```

## Handlebars.js

Précompilation et fonctionnalités supplémentaires par rapport à _Mustache._

```markup
{{#if data}}
<div>
    <h1> {{title}} </h1>
    <ul>
        {{#data}}
        <li title="job: {{job}} status: {{status}}">
            {{name}}
        </li>
        {{/data}}
    </ul>
</div>
{{/if}}
```

[https://www.bearfruit.org/2014/01/20/node-js-template-showdown-5-options-compared/](https://www.bearfruit.org/2014/01/20/node-js-template-showdown-5-options-compared/)

{% embed data="{\"url\":\"https://www.bearfruit.org/2014/01/20/node-js-template-showdown-5-options-compared/\",\"type\":\"link\",\"title\":\"Node.js template showdown - 5 options compared - Bearfruit\",\"description\":\"Five of the most popular Javascript and Node.js template engines compared - Jade, EJS, JSHTML, Mustache/Hogan.js and Handlebars.js.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.bearfruit.org/files/2014/05/vine-favicon.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.bearfruit.org/files/2013/12/7043958085\_54c2a01fd9\_b.jpg\",\"width\":1024,\"height\":682,\"aspectRatio\":0.666015625}}" %}

