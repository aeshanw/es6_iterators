# ES6 Iterators

This topic discusses the material taken from http://exploringjs.com/es6/ch_iteration.html

## Pre-ES6

This covers the new enhancements to Looping in ES6, namely the Iterators.

In ES5 we might recall the use of looping like:

```
var arr = ["1" ,"2", "3", "4", "5"];
for(var index=0; index < arr.length; index++){
  console.log("item:",arr[index]);
}

```

Very similar to traditional loops in languages like C or Java.

## Iterators

An iterator essentially allows you to traverse a data-structure sequentially via a method like

```
iterator.next() //returns the next element in sequence.
```

ES6 currently has iterator-support for 

* Arrays
* Strings
* Maps
* Sets

You can apparently iterate over a tree datastructure tho what ES6 would do is basically squash it into a linear structure before iterating over it.

### Getting the iterator
The book given an `Array` as a simple example of how one would get a `Iterator` from a data structure.
```
const arr = ['a', 'b', 'c'];
const iter = arr[Symbol.iterator](); // Array Iterator {}
```

But as it mentions that any of the above data types (which all implment the `Iterable` interface), would expose a similar method.

So lets try a `String`.

```
const str = "Hello World!";

const strIter = str[Symbol.iterator](); // StringIterator {}
```

So it's safe to assume the method should apply to the rest.

__Note: the iterators returned are of different 'types' i.e: different prototypes.__

```
strIter 
StringIterator {}__proto__: String Iterator
iter
Array Iterator {}__proto__: Array Iterator
```

### Iterating with an iterator

Now that we have a means of traversing a data type of our choice, let's try it out with some exercises:

```
iter.next()
{value: "a", done: false}
strIter.next()
{value: "H", done: false}

iter.next()
{value: "b", done: false}
strIter.next()
{value: "e", done: false}
```

Using the iterators we got in the earlier example we're able to traverse through the data structures in a  `linear` fashion. We have no means of reversing the direction of traversal (which would probabaly return a re-invokation of the `iterator method`)

#### Example (using let insted of const)

```
let strIter2 = str[Symbol.iterator]();

.....

strIter2 = str[Symbol.iterator](); //reset iterator
StringIterator {}
strIter2.next()
{value: "H", done: false}
```

#### Iterable computed data

All `Iterable` data structures have methods which return iterable objects which may save the effort of writing custom code for traversal purposes.

```
const arr = ['a','b','c'];

arr.entries(); // Array Iterator {}

arr.keys();

arr.values();

for (const x of arr.entries()){ 
  console.log("%s : %s",x[0],x[1]);
}

//output
0 : a
1 : b
2 : c

```


#### Iterating over Plain Objects

Previously in ES5, for lack of a better data structure we used `Objects` as rudimentary `Maps`. Although Objects (via their proprties) were iterable back then to support such methods, this feature has been removed in ES6.

```
const data = {
  name: 'hello',
  count: 2
}
for (const x of data) { // Uncaught TypeError: data is not iterable
    console.log(x);
}
```

Note: Though indirectly-iterating over object properties are still possible via tool functions like `objectEntries()`.

### Language constructs that are Iterable

Of the complete list which support the iteration protocol:

* Destructuring via an Array pattern
* for-of loop
* Array.from()
* Spread operator (...)
* Constructors of Maps and Sets
* Promise.all(), Promise.race()
* yield*

I will discuss a few choice-picks:

#### Array.from()

Basically an Array-ify method for all `Iterable` data structures.

It works for:

```
Array.from(new Map().set(false, 'no').set(true, 'yes'))
Array.from({ length: 2, 0: 'hello', 1: 'world' }) // (2) ["hello", "world"]

```

But doesn't work on Plain Objects

```
const data = {
  name: 'hello',
  count: 2,
  color: '#ffff'
}

Array.from(data); // []
```

#### Spreads ...

Since `...` allows you to insert an array (i.e: values of an iterable) into another array:

```
const arr = ['b', 'c'];
['a', ...arr, 'd']
['a', 'b', 'c', 'd']
```

It should allow the same of any `Iterable`:

```
let iterable = new Map().set(false, 'no').set(true, 'yes')
let arr = ['a', ...iterable, 'd'] //  ["a", Array(2), Array(2), "d"]

```

#### Maps & Sets

You can 'magically' construct and initialize Maps by passing in params as `Array of Arrays` (i.e: `2D Array`):

```
const map = new Map([['uno', 'one'], ['dos', 'two']]);
map.get('dos')
```

The same applies to Sets (tho with a `1D` rather than a `2D Array`).

```
const set = new Set(['red', 'green', 'blue']);
set.has('yellow')
```

#### Promises

Both `Promise.all` & `Promise.race` accept any `Iterable` object containing Promises.

So insted of a the traditional `Array` used in such examples we could just as easily pass in a `Set`.

```
let promise1 = new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve("Success!"); // Yay! Everything went well!
  }, 250);
});

let promise2 = new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve("Success!"); // Yay! Everything went well!
  }, 500);
});

let promiseSet = new Set();
promiseSet.add(promise1).add(promise2)

Promise.all(promiseSet).then(function(){
  console.log("All done!");
});


```

Same applies to `race` using a `Map`

```
let promiseMap = new Map();

promiseMap.set("promise1", new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve("Promise1!"); 
  }, 3500);
}))
promiseMap.set("promise2",new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve("Promise 2!");
  }, 250);
}))

Promise.race(promiseMap).then(function(result){
  console.log("The winner is:", result);
});

```


### Implementing iterables

I considered going into this but as it notes that the preferred ES6-way to implement iterables would be via `Generators`. I thought it best to skip over this section till we cover the `Generators` chapter.

# More examples of iterables

Basically a collection of tool functions that assist in iterating through non-iterable and supporting features not supported by ES6 Iterables. 

# Conclusion

I didn't have time to go into `21.6 More examples of iterables` So I'll be ending it here.
