# Closures

## **¿What is a closure?**<br>
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).<br>
In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

A closure is a function having access to the parent scope, even after the parent function has closed.

## **Give me an example of closure**. 

function hike(){

    let kms=5                //parent scope
    
    function changekms(){    //this is a inner function, a closure
    
        kms=kms*3;
        
        console.log(kms)
        
    }
    
    return changekms
    
}

hike()                  // return a function <br>
hike()()               // 15                                             
console.log(hike())    // function changekms(){kms=kms*3; console.log(kms)}

## **What is ()() in code?**

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

## **Move the variable after the closure (the function inside the function) and explain what happens**.

it works correctly because of the *lexical enviroment*, this has two main components: environmentRecord and reference to outer environment.

function hike(){
    
    function changekms(){
    
        kms=kms*3;
        
        console.log(kms)
        
    }
    
    var kms=5;
  
    return changekms
}

hike()() //15 <br>
console.log(hike()) //function changekms(){kms=kms*3; console.log(kms)}

So it does not matter if the variables from main functions are after the inner function/closure, but the they can not be declared after return because it will be a ReferenceError: "Can not access 'kms' before initialization".

## **Change var for let and explain why the logic is not affected**

function hike(){
    
    function changekms(){
    
        kms=kms*3;
        
        console.log(kms)
        
    }
    
    let kms=5;
  
    return changekms
}

hike()() //15 <br>
console.log(hike()) //function changekms(){kms=kms*3; console.log(kms)}

In this example we could think that the code will break because of the hoisting but it is not true. <br>
In closures, the hoisting does not affect, so as I menctioned before in the last example, this is possible thank to *lexical enviroment*.

## **Scope chain, an example of it, how many closures can we nest**

Every closure has three scopes:<br>
- Local Scope (Own scope)<br>
- Outer Functions Scope<br>
- Global Scope

Nested functions have access to the scope "above" them.

function market(){

    let iva=1.16;
    
    function products(prod){
    
        let costs={tortilla: 15, soda: 20};
        
        var item=prod;
        
        function findprice(){
        
            let prod_availables=Object.entries(costs);
            
            switch (item) {
            
                case prod_availables[0][0]:
                
                    var price = prod_availables[0][1]*iva;
                    
                    console.log("El costo con iva de " + item +" es: " +price);
                    
                    break;
                    
                case prod_availables[1][0]:
                
                    var price = prod_availables[1][1]*iva;
                    
                    console.log("El costo con iva de "+ item +" es: " +price);
                    
                    break;
                    
                default:
                
                    console.log("This product does not exist, choose another");        
            }            
            
        }
        
        return findprice
        
    }    
  
    return products
}

market()("soda")() //"El costo con iva de soda es: 23.2"

There is not a number of nested closures that we can use, it depends that you want your code does, we can use nested closures or closures at the same level.

## **They are conflicts between the closure and the global scope?**

## **Advantages of closures**.

- Closures allows us to create modules, they let you define private implementation details (variables, functions) that are hidden from the outside world, as well as a public API that is accessible from the outside.
- Closure enables the use of nested functions that are used to get the values created in the execution context of that of the parent function.
- They can prove as a perfect solution while solving a problem of hierarchy in any program.
- The purpose of a closure is to extend the life cycle of a local variable. After the function is executed, the local variable cannot be released by memory, and then the external can access the variable.

## **¿What is data hiding and encapsulation?**

Data hiding is the ability of objects to shield variables from external access. It is a useful consequence of the encapsulation principle.<br>
JavaScript does not have syntax-level encapsulation. All properties of an object are visible. However, there do exist various patterns to ensure data encapsulation: *Singletons* and the *Module Pattern*.<br>
The difference between Data Hiding and Data Encapsulation is that Data hiding refers to a process, and Data Encapsulation is a part of a sub-process of that process.

## **Give me an example of privacy with closures**.



## **What happens if you create two counters with the same closure?**


## **How can we add more functions as a decrement counter? Give an example of it**.



## **What are the disadvantages of closures?**

- Variables used by closure will not be garbage collected.
- Memory snapshot of the application will be increased if closures are not used properly.
