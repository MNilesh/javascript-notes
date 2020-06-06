 # Shadow DOM
 
 
 ```
 <div id="shadowHost"></div>  
 ```
 
 ```
var host = document.querySelector('#shadowHost');
var shadowRoot = host.createShadowRoot();
var div = document.createElement('div');
div.textContent = "Hello";
div.className ="red";

shadowRoot.appendChild(div);
```

The above won't leak its style outside.
