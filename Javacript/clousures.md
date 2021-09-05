# Clousures  
Clousures in JS is a concept related to functions. Particularly, it refers to the scope of functions, that is the variables and methods that
can be accessed from within the function body.

## Lexical Scope: Accessing outer scope variables 
When creating a new function either via function declaration or function expression, inside the function body we can access variables and methods 
outside it thanks to Javascript's lexical scoping. The lexical scope or lexical environment is composed of the inner function members, as well as its
surrounding members, that is, the outer environment. Lets see this in action in the following example code.

```javascript
//Outer scope
const homeCity = 'Popayan';

const fetchWeather = () => {
    //inner scope
    const url = 'CurrentWeather.com'
    console.log(`Fetching weather data for ${homeCity} from ${url}`);
}
//Console output:
//"Fetching weather data for Popayan from CurrentWeather.com"
```
Here we can see how we get access to the homeCity variable from within our fetchWeather function body. The lexical environment created for the fetchWeather function
includes its own function body, as well as the surrounding environment, in this case the global scope.

## IIFE - Shielding against polluting the global scope
Sometimes we want to write some initialization code, but we don't want to pollute the global scope when creating new variables/methods. To circunvent this issue, 
we can take advantage of the IIFE concept. In a nuthsell, an IIFE, or immediatly invoked function expression is a function that gets called immediatly after begin created, effectively creating a self-contained lexical environment.  

Following the previous example, let's imagine we need to fetch some data from a different url before using CurrentWeather.com. We can use an IIFE to acomplish this.  

```javascript
//Outer scope
const homeCity = 'Popayan';

const fetchWeather = () => {
    //inner scope
    const url = 'CurrentWeather.com'
    
    (function(){
        const url = 'OtherCurrentWeather.com';
        console.log(`Initializating app from ${url}`);
    })()

    console.log(`Fetching weather data for ${homeCity} from ${url}`);
}

//Console output:
//"Initializating app from OtherCurrentWeather.com"
//"Fetching weather data for Popayan from CurrentWeather.com"
```
What's different here is the anonymous function created and called immediately. The new code uses the **Grouping Operator**, an **anonynomous function**, and a set of
parenthesis **()** to call the function right after being created. This pattern ensures tha the lexical environment is isolated from the global scope, thus we dont have access to the url variable defined in the inner scope, reason why the second console.log outputs the same text.

## Practical Clousures
A very common mistake when using clousures happens when assigning function clousures as callback functions to events. Imagine we have an HTML document with a single header and three buttons: 10px, 15px and 20px. On clicking any button the font size of the document should change. Let's first see the HTML document code.

```html
<html>
    <head></head>
    <body>
        <h1 id="title">The Lord of the Rings saga is a masterpiece</h1>
        <button id="btn10">10px</button>
        <button id="btn15">15px</button>
        <button id="btn20">20px</button>
    </body>
</html>
```

```javascript

//create function declaration 
function fontSizeCallbacks (){
    var buttonData = [
        { "id": "btn10", "size":"10px" },
        { "id": "btn15", "size":"15px" },
        { "id": "btn20", "size":"20px" }
    ]

    for (var i=0; i<buttonData.length; i++){
        var item = buttonData[i]
        document.getElementById(item.id).onclick = function(){
            document.getElementById("title").style.fontSize = item.size;
        }
    }
}

//call function
fontSizeCallbacks()
```

After running this code we realize it does not work as expected. The problem relies on function clousure that is being assinged to the onclick event. 
More specifically, the value of item.size is calculated only when the callback function is called, which happens when the onclick event of any of the three 
buttons is triggered. Then, because the item variable is left pointing to the last js object of the buttonData array, we dont see any font size change in the 
document when we click any of the buttons. There are multiple ways we can solve this issue we, let's see some of them.

### Using a function clousure
We can use a function clousere to get around the issue previously found. Here we will use a function clousure as our callback function. This clousre will return an anonymous function whose lexical environment is unique. 

```javascript

//create function declaration 

function makeCallback(size){
    return function(){
        document.getElementById("title").style.fontSize = size; //from here we can access the size parameter, which is unique to this lexical environment
    }
}

function fontSizeCallbacks (){
    var buttonData = [
        { "id": "btn10", "size":"10px" },
        { "id": "btn15", "size":"15px" },
        { "id": "btn20", "size":"20px" }
    ]

    for (var i=0; i<buttonData.length; i++){
        var item = buttonData[i]
        document.getElementById(item.id).onclick = makeCallback(item.size);
    }
}

//call function
fontSizeCallbacks()
```
Now we see each button changes the title's font size. Thanks to JS' lexical scoping we were able to create an isolated environment to each callback function execution.

### Using IIFE  
Another way to approach this situation is through IIFE. In this case we create a self-contained function clousure which is immediatly invoked after being created. This effectively defines unique lexical environments for each iteration of the for loop.  

```javascript

//create function declaration 

function fontSizeCallbacks (){
    var buttonData = [
        { "id": "btn10", "size":"10px" },
        { "id": "btn15", "size":"15px" },
        { "id": "btn20", "size":"20px" }
    ]

    for (var i=0; i<buttonData.length; i++){
        var item = buttonData[i]
         (function(item){
            var item = buttonData[i]
            document.getElementById(item.id).onclick = function(){    
                document.getElementById("title").style.fontSize = item.size;
            }
        })()
    }
}

//call function
fontSizeCallbacks()
```

### Using ES6 let keyword
ES6 introduced several features, including the let keyword. Variables defined with let are blocked-scoped, meaning their value is unique to the current iteration block. This is indeed the easiest solution to the problem at hand, we can simply take the original code an replace the item variable creation to use let instead of var
and the code will work as expected.

```javascript

//create function declaration 
function fontSizeCallbacks (){
    var buttonData = [
        { "id": "btn10", "size":"10px" },
        { "id": "btn15", "size":"15px" },
        { "id": "btn20", "size":"20px" }
    ]

    for (var i=0; i<buttonData.length; i++){
        let item = buttonData[i]
        document.getElementById(item.id).onclick = function(){
            document.getElementById("title").style.fontSize = item.size;
        }
    }
}

//call function
fontSizeCallbacks()
```

### Bonus
Understanding function clousure and lexical environment is key to learning more sophisticated JS development topics such as Design Patterns. In particular, the Module pattern relies heavily in a good understanding of function clousures and lexical environments.

## Conclusions
- Function clousure is an important concept in JS as it defines inner and outer environments we must consider when writing JS code.
- A lexical environment is the function clousure scope. 
- We can create self-contained lexical environments by means of IIFE.
