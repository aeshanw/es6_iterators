# ES6 Iterators

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


# Conclusion

I didn't have time to go into `21.8 The ECMAScript 6 iteration protocol in depth` So I'll be ending it here.
