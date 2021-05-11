<h1>ES6 Javascript expressions </h1>
<p>JS expressions are a new feature shipped by ES6 specification. 
As defined by MDS, a "javascript expression is any unit of code that resolves to a value".
Even though this can get really complex, on a nutshell it means that anything that returns a single value without "complex" processes may be considered an expression. <br>
For instance 
    if(val>10):
        return 100:
    else:
        return 200
is not an expression because even though it resolves to an int value, it requires some further 
statement evaluation (if statements in this case).
5+5 or Array.reduce((a,b)=>a+b,0) are both expressions.
</p>
<h3>When should I use them?</h3>
In react application development js expressions are particularly useful for embedding js code logic into html code. Say for example that we want to render the current year inside a p tag.
Using js expressions we can do this by writing: <br>
<strong> &ltp&gt {new Date().getFullYear()} &lt/p&gt </strong> <br>
This allows us to incorporate the resulting year as text inside the p tag.