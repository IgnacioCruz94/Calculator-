# Closures

¿What is a closure?
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). 
In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

A closure is a function having access to the parent scope, even after the parent function has closed.

Give me an example of closure. 

function hike(){
    let kms=5                //parent scope
    function changekms(){    //a closure
        kms=kms*3;
        console.log(kms)
    }
    
    return changekms
}
hike() // 15

What is ()() in code? 
The double parentheses allows us to execute the internal functions of the main function, in addition to being able to introduce arguments in internal functions that require it.

