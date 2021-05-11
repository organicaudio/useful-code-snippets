# Vue JS

[Vue style guide](https://vuejs.org/v2/style-guide/#Avoid-v-if-with-v-for-essential)
[Vue instance properties](https://vuejs.org/v2/api/#Instance-Properties)

## vue cli

[Vue clie](https://cli.vuejs.org/) allows to easily scafffold a vue project:

- install vie `npm install -g @vue/cli`
- create project:
  -  `vue ui` is ui guided
  -  `vue create my-project` 

To set [environmental variables in vue](https://cli.vuejs.org/guide/mode-and-env.html) during transpile time:

- use `.env-XXX` files in the root of the project to define variables
  -  `.env` global definition
  -  `.env.local` ignored by git
  -  `.env.development` default used by `npm serve`/`vue-cli-service serve`
  -  `.env.production` default used by `npm build`/ `vue-cli-service build`
- variables need to starts with `VUE_APP_`
- usage in code with `process.env.VUE_APP_`

## overview

- the vue core library focuses on view layer only
- can be used via cdn or with vue-cli scafffolded project (with webpack, babel etc.)
- allows to bind js variables with html content
- reactivly change content on html page when js variable changes. 
- No need for direct DOM manipulation
- declarative rendering via template syntax in html `{{}}`
- two way binding via `v-model` writable html fields
- v-if for conditional rendering
- v-for for loops
- v-event for binding events to function. The feature here is that the function do not need to manipulate the dom directly.
- concept which works like Custom Elements of the web components standard

## vue instance

- You need at least one **Vue instance** to start a application.
- Loosely coupled to the Model–view–viewmodel (MVVM) and the **Vue instance is the viewmodel(vm)** and the html the view.
- The component system also use Vue instances
- the **`data` property** of a Vue object is used to reactly injected into the dom. (you can not define new fields in data after the page was rendered)
- Vue **instance properties** relevant ([full list](https://vuejs.org/v2/api/#Instance-Properties)):
    - data
    - el
    - computed
    - methods
    - watch
- **vue lifecycle** is shown in this [graphic](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram). An overview of the lifecylce is:
    - set up data observation
    - compile the template
    - mount the instance to the DOM
    - update the DOM when data changes
- there are **lifecylce hooks** for the different events. These are functions with a predefined name (like created or mounted). Here is the [full list](https://vuejs.org/v2/api/#Options-Lifecycle-Hooks).

## template syntax

- allows to declaratively bind the rendered DOM to the vue instance
- Vue templates are valid HTML
- Vue uses a virtual DOM to optimize the operations on the real DOM


Syntax:

- bind (uninterpreted/escaped) **text** with mustache syntax: `{{}}`
- bind **html** with: `v-html` directive
- bind **attributes** with: `v-bind:` before the attribute or just `:`
- bind **events** with: `v-on` before the event name or just `@`
- Use (one) **javascript expression** between curlys: `{{ text.split('') }}` (They do have access to the data property and a [few global](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9))
- **directives** link to a javascript expression and are started with `v-` (predefined examples are v-for, v-if)
- some directives take **arguments** (like v-bind(:<attribute>="<value>") does which takes the attributes value as an argument)
- directives can also take **dynamic arguments** which are javascript expression in square brackets. An example is `<a v-bind:[attributeName]="url"> ... </a>`. But there are constraints on this feature.
- **modifiers** are postfixes of directives which starts with a `.`

## computed properties

- Have the same function as the inline javascript expression between curlys in html
- Allows to move this code to a function defined inside the `computed` field of the Vue instance
- called with just the name of the computed expressions (so without the braces `()` of the funciton)
- If a field inside the data field changes vue will automagically update all bindings of a computed properties which use this field as well
- unfavourable but more flexible alternatives:
    - vue instance methods, because computed properties are cached
    - watched properties, because their sytanx is imperative and tends to be verbose

## style binding

- v-bind has a special features when binded to `class` and `style` attribute
- **toggle a single class** with a isActive property: `v-bind:class="{ preDefinedClass: isActive }"`
- **toggle multiple classes**: `v-bind:class="{ preDefinedClass: isActive, 'my-class-name': show }"`
- **have static class** and toggled class: `class="static"  v-bind:class="{ classDefinedInProperty: isActive }`
- it is also possbile to define **no inline expression but a data property or a computed expression** for the class toggling logic
- **add list of classes** with an array syntax : `v-bind:class="[class1, class2]"`
- *bind to style attribute* is similar [see](https://vuejs.org/v2/guide/class-and-style.html#Binding-Inline-Styles)

## conditional rendering and list rendering

- add `v-if` attribute to a element to conditionally render it
- has effect on all nested elements
- there are also `v-else` and `v-else-if`
- allows to build input forms which do not delete its content when the user change to a different option
- if you want to prevent this behaviour you need to add a `key` attribute
- `v-show` is similar to `v-if` but it keeps the elements in the dom at all times (only toggles the display CSS property)

## list rendering

- use `v-for="item in items"` to print an elements for every item in the items field of data
- vue only propagate changes to the DOM when the following methods are used: push(), pop(), shift(), unshift(), splice(), sort(), reverse()
- for **filtering** iterate on computed properties instead of the property directly

## events

- use `v-on:<event>` or `@<event>` directive 
- you can use inline exrepssion or a directive call in the vue instance to define the behaviour when the event happends
- to pass the event reference to the method handler add a `$event` parameter in the template

## form input bindings

- you can two way data bind a input field inside a form element with `v-model`
- the initial value will be picked from the data binding not the value in the html template 
- the events to update a data binding from template are:
    - input event on the value property for text and textarea 
    - change event on the checked property for checkboxes and radiobuttons
    - change event on the value property for select fields
- there are [modifiers](https://vuejs.org/v2/guide/forms.html#Modifiers) to add some behavoiur to the data binding (.lazy, .trim etc.)

