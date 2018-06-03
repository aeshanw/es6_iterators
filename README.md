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

# Conclusion

I didn't have time to go into `21.8 The ECMAScript 6 iteration protocol in depth` So I'll be ending it here.
