# Web Components

Web component can be used to isolate each layouts into separate logical entity.

## Creating Custom Elements

### The HTML
To create any custom tag, we perform following steps:
We create the tag name of our choice in which new words are separated with hypens.

 ``` 
 <user-card name="John Doe">
     </user-card> 
  ```
  
 ### The JS
 We first create its class and extend it with HTMLElement. This comes with many callback methods of which 2 are important.
 1. connectedCallback    -> called when the element is added to the DOM.
 2. disconnectedCallback -> called when the element is disconnected from DOM.
 
 To access the name attribute mentioned in the previous code, we use standard getAttribute method as shown below.
 
 ```
 class UserCard extends HTMLElement{
  constructor(){
    super();
    this.innerHTML = `<h3>${this.getAttribute('name')}</h3>`;
  };
  ```
 After creating the element class, we attach it to the DOM:
  ```
  window.customElements.define('user-card',UserCard);
  ```
  
 Adding Styles using style tag will even style the main DOM's h3 elements. To have an encapsulated style, we use the concept of Shadow DOM. 
 We first create a template tag and attach all the layout to it.
 ```
 const template =document.createElement('template');
template.innerHTML = `
<style>
  h2{
    color:coral;
  }
</style>
<div class="user-card">
  <h2></h2>
  <button id="toggle-info">Hide Info</button>
</div>

`;
 ```
 This will ensure that the style remains intact to this html only.
 
 Inside the constructor we create the shadow DOM and clone the template here:
 
 ```
    this.attachShadow({mode: 'open'});
    this.shadowRoot.appendChild(template.content.cloneNode(true));
    this.shadowRoot.querySelector('h2').innerText=this.getAttribute('name')
 ```
 
## Creating Slots
 Slots are used to pass data from the tag to the element class. It allows us to pump in dynamic data inside the template.
 Slots can be single slot or multi-slot.
 For multi-slot, we define **slot** attirbute with a value.
### The HTML
 ``` 
 <user-card name="Akkkiii">
      <div slot="email">akki@gmail.com</div>
      <div slot="phone">999-999-4454</div>
  </user-card> 
  ```
### The JS
  Inside the template layout, we use the following:
   ```
  <p><slot name="email"/></p>
  <p><slot name="phone"/></p>
  ```
  This will automatically populate the values passed in the HTML here in JS.
  
  We can attach event listeners too. Shown in the final code.

## Final Code:
### The HTML
```
  <user-card name="Akkkiii">
      <div slot="email">akki@gmail.com</div>
      <div slot="phone">999-999-4454</div>
  </user-card>
```
### The JS
```
const template =document.createElement('template');
template.innerHTML = `
<style>
  h2{
    color:coral;
  }
</style>
<div class="user-card">
  <h2></h2>
  <p><slot name="email"/></p>
  <p><slot name="phone"/></p>
  <button id="toggle-info">Hide Info</button>
</div>

`;


class UserCard extends HTMLElement{
  constructor(){
    super();

    this.attachShadow({mode: 'open'});
    this.shadowRoot.appendChild(template.content.cloneNode(true));
    this.shadowRoot.querySelector('h2').innerText=this.getAttribute('name')

  };

  toggleInfo(){
    console.log('clicked');
  }
  connectedCallback(){
      this.shadowRoot.querySelector('#toggle-info').addEventListener('click', ()=>{ this.toggleInfo()})
  }

  disconnectedCallback(){
    this.shadowRoot.querySelector('#toggle-info').removeEventListener();
  }
};

window.customElements.define('user-card',UserCard);
```

