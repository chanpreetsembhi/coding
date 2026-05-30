#### HTML File Structure

```html
<div id="products-wrapper"></div>
```

#### JavaScript File Structure

1. Create a array of card inner text.
2. Select Dom element based on html file` class` or `id`.
3. Create a const of empty Array.
4. Looping Through `Products` Array with `forEach()` method.
5. Create a function who create card.
    - Create a element and store in a const variable `document.createElement('html Tag')`.
    - Add class in that const variable `variable.className = 'classes'. 
    - Add inner html in that const variable =` variable.innerHtml = ``.`
    - Then return create element variable in inside the function.
6. Declared that function inside the `forEach()` method to create that Card in a const variable.
7. Add Function const variable in empty array which we made in step `3` with `variable.push()`.
8. Then Append or show in html page with `variable.appendChild()`
```js
const products = [
    {
        name: 'Sony Playstation 5',
        url: 'img/playstation_5.png',
        category: 'games',
        price: 499.99,
    },
    {
        name: 'Samsung Galaxy',
        url: 'img/samsung_galaxy.png',
        category: 'smartphones',
        price: 399.99,
    },
];

// Select Dom Elements
const productWrapper = document.getElementById('products-wrapper');

// Init Product Element Array
const productElements = [];

// Loop over product and create a element
Products.forEach((product) => {
   const ProductElement = createProductElement(product);
   const ProductElements.push(ProductElement);
   const ProductElements.appendChild(ProductElement);
})

// Create product element
function createProductElement(product){
   const productElement = document.createElement('div');
   productElement.className = 'item space-y-2';
   productElement.innerHTML =  '<div>Card</div>';
   
   return productElement;
}
```