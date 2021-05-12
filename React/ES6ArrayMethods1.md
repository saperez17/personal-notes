
Map
array method for applying a mapping function to each array value. A very simple example is a doubling mapping function.

let myArr = [2,4,6]
const doubledArr = myArr.map((val)=>{val*2})

In React development the map array method is useful for mapping data to Rect components. Suppose we have a Card component that takes a single
prop, name. Now, we have an array containing a bunch of name for which we want to create a Car for.

let contacts = ["dad", "mom", "neighbour"]

With the map method we could do something like this:

contacts.map((name)=>{<Card name={name}/>})

Note how succint this looks like. Here we are using ES6 arrow functions as the argument for the map method. This arrow function takes
the current name and return a Card component, passing the name as a prop argument. 

Filter
The filter array method is another useful method included in the ES6 version. The filter, as its name suggests, is used for filtering an array.
Simply put, it helps us to get rid of undesirable data. For instance, say we have the following array from which we want to get rid of the even 
numbers:

let numbers = [1,2,3,4,5,6];

We could use te filter method like so:
let oddNumbers = numbers.filter((val)=>val%2!=0)

The array function returns only the numbers which satisfy the given condition, in this case all numbers for which the module to two is
different than zero.

Bonus:
The filter method can also be used to filter js objects. In fact, this is the most common case. Let's see how this works with an example.
Suppose we have the following js object array of cars.

let cars =  [
	{brand: "ford",
	price:25000
	milage: "12000",
	year:2019
	},
	{brand: "ford",
	price:20000
	milage: "10000",
	year:2018
	},
	{brand: "chevrolet",
	price:28000
	milage: "9000",
	year:2020
	},
]

Now, we would like to get the ford objects cars out of the cars array. Using filter we could do it like this:

let fordCars = cars.filter((car)=>car.brand=='ford')

You could even have nested properties and it would still work.


Reduce
Lastly, the reduce method is used to output a single value after iterating over the entire array. Using the same numbers array from the filter method 
section we could find its sum using the reduce method as follows:

let sum = numbers.reduce((iterator, currentVal)=>iterator + currentVal,0)

This would result in sum being equal to 21. Notice the second parameter I used to the reduce method, 0. This number is optional and is the initial value.
By default is zero, so you don't need to pass it in explicitely if you are not worried about setting an initial value. But if we do it and set it to 1,
then the sum would be equal to 22.


Find & FindIndex
