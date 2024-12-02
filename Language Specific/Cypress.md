### Alias
When we are saving an alias, cypress only saves the original selector as the `"variable"` not the jquery object.
For example, `cy.get('.gg').as(al)` the alias `@al` holds the selector `.gg`
So essentially, it is the same as running `cy.get('.gg')` again.
So **Beware,** even if any attributes of the element, or the children of the element is modified but original selector isn't then the element can be found! 

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