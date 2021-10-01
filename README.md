# Closures

**¿What is a closure?**<br>
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).<br>
In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

A closure is a function having access to the parent scope, even after the parent function has closed.

**Give me an example of closure**. 

function hike(){

    let kms=5                //parent scope
    
    function changekms(){    //a closure
    
        kms=kms*3;
        
        console.log(kms)
        
    }
    
    return changekms
    
}

hike()                  // return a function <br>
hike()()               // 15  <br>                                               
console.log(hike())    // function changekms(){kms=kms*3; console.log(kms)}

**What is ()() in code?**

The double parentheses allows us to execute the internal functions of the main function, in addition to being able to introduce arguments in internal functions that require it.

function hike(){

    let kms=5;
    
    function changekms(number){
    
        kms=kms*number;
        
        console.log(kms)
        
    }
    
    return changekms
    
}

hike()(4) // 20

**Move the variable after the closure (the function inside the function) and explain what happens**.

it works correctly because of the lexical enviroment, this has two main components: environmentRecord and reference to outer environment.




