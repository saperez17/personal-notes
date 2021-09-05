# Hoisting  
Hoisting in js referes to the ability to call a method, or variable before **it was created**.  

## Function declaration vs Function expression
A simple example of hoisting would be that of function expression vs function declaration.
While functions declarations are hoisted, function expression are not. Take a look the the
following examples.

```javascript

const buildBridge = build('Bridge'); // -> this works just fine as the build function declaration is hoisted

build1('Bridge') //this gives a Syntax error? as build1 function expression is not hoisted

//function declaration
function build(structure){
    console.log(`Building new structure: ${structure}`)
}

//function expression
const build1 = (structure)=>{
    console.log(`Building new structure: ${structure}`)
}

```