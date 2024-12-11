### Alias
When we are saving an alias, cypress only saves the original selector as the `"variable"` not the jquery object.
For example, `cy.get('.gg').as(al)` the alias `@al` holds the selector `.gg`
So essentially, it is the same as running `cy.get('.gg')` again.
So **Beware,** even if any attributes of the element, or the children of the element is modified but original selector isn't then the element can be found! 
> [!danger] Aliases Don't Always have the *Selector* Property
> An alias will only have the `selector` property when it is assigned through commands that work with selectors, such as `cy.get()`, `cy.find()`, and similar commands. These commands yield elements with a `selector` property, which is accessible when the alias is used.
> 
> > [!bug] A common pitfall happens using `.each()`
> ```js
> cy.get(elements).each((el,index) => {
>	cy.wrap(el).as("alias").debug()
>	// logging the subject, we can see that, 
>	// the `subject` object doesnt have any selector property 			
> })
> ```
> You have to handle this in a different way.

### JQuery Objects
JQuery saves its object in memory and whenever any function modifies the object, the object is passed by reference.
So in the following example,
```js
console.log($img) // img#therap > 0: id: 'gg'
$img.attr('id','gg')
console.log($img) // img#gg > 0: id: 'gg'
```
Even though in the first log id should have been `therap` **instead** browsers show it as `gg`.

###  `cypress-pipe` Plugin
> [npm Package](https://www.npmjs.com/package/cypress-pipe)
> [When can the test click?](https://www.cypress.io/blog/when-can-the-test-click)


###  Removing the XHR Logs
> [Hide XHR Call Logs](https://stackoverflow.com/questions/71357705/hide-xhr-calls-on-cypress-test-runner)
> [Gist link](https://gist.github.com/simenbrekken/3d2248f9e50c1143bf9dbe02e67f5399)

Add the following code, in `cypress/support/e2e/js`
```js
const hideXHR = true // toogle to show/hide
if (hideXHR) {
  const app = window.top;
  if (!app.document.head.querySelector('[data-hide-command-log-request]')) {
    const style = app.document.createElement('style')
    style.innerHTML =
      '.command-name-request, .command-name-xhr { display: none }'
    style.setAttribute('data-hide-command-log-request', '')
    app.document.head.appendChild(style)
  }
```

This can significantly improve the performance of cypress as the browser doesn't need to load all those logs.