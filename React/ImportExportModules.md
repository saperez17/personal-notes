<h1>ES6 Import, Export and Modules</h1>
ES6 ships a new way to import, export and define modules. These are different from what we
know in Node.js and, indeed, are more intuitive and the prefered method when working in
react development.

<h2>Import</h2>
The new <strong>import</strong> keyword is used to import modules. Here's how we use it.

#Defult export
import module_name from './my_module.js' <br>
where module_name can be the module's default export name, or a custome one.

Say for instance we have a math.js module with the following code:

//math.js
function add(x,y){
    return x+y
}
export default add;

And a main.js file inside the same directory as follows:

//main.js
import add from './math'

As you can see, inside main.js we are importing the add function form math.js using the exact same name used to export it. However, we can use any name we want:

//main.js 
import customAdd from './math'
<br>

<h2>Export</h2>


<h2>Modules</h2>






