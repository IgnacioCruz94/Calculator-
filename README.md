# Closures

## **¿What is a closure?**<br>
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).<br>
In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

A closure is a function having access to the parent scope, even after the parent function has closed.

## **Give me an example of closure**. 

function hike(){

    let kms=5;                //parent scope
    
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

There is no conflict between the variables, each one corresponds to a different scope, as shown in the example:<br>

#### *Example 1*
const global_variable="Global scope";

function Ignacio(){

    const global_variable="function scope";
    
    function closure(){
    
        const global_variable="local scope";
        
        console.log(global_variable)
    }
    
    return console.log(global_variable)
}

Ignacio() //"function scope"

console.log(global_variable) //"Global scope"

#### *Example 2*

const global_variable="Global scope";

function Ignacio(){

    const global_variable="function scope";
    function closure(){
        const global_variable="local scope";
        console.log(global_variable)
    }
    
    return closure
}

Ignacio()() //"local scope"

console.log(global_variable) //"Global scope"

## **Advantages of closures**.

- Closures allows us to create modules, they let you define private implementation details (variables, functions) that are hidden from the outside world, as well as a public API that is accessible from the outside.
- Closure enables the use of nested functions that are used to get the values created in the execution context of that of the parent function.
- They can prove as a perfect solution while solving a problem of hierarchy in any program.
- The purpose of a closure is to extend the life cycle of a local variable. After the function is executed, the local variable cannot be released by memory, and then the external can access the variable.
- We can use closures to create another functions.

## **¿What is data hiding and encapsulation?**

Data hiding is the ability of objects to shield variables from external access. It is a useful consequence of the encapsulation principle.<br>
JavaScript does not have syntax-level encapsulation. All properties of an object are visible. However, there do exist various patterns to ensure data encapsulation: *Singletons* and the *Module Pattern*.<br>
The difference between Data Hiding and Data Encapsulation is that Data hiding refers to a process, and Data Encapsulation is a part of a sub-process of that process.

## **Give me an example of privacy with closures**.

function test(){

    var text="try to print me on console ";
    
    function print(){
    
        console.log(text)
        
    }
    
    return print
    
 }
 
 test()() //"try to print me on console " 
 
 console.log(text) //ReferenceError: text is not defined

## **What happens if you create two counters with the same closure?**

If I can find an ocassion to do it, I will have a function factory, I need to assign to new variables the the function factory, for example:

function counterBuilder(n){

let counter=100;

   function decrement(){
   
     counter=counter-n;
   
     console.log(counter)
   
   }
   
   return decrement

}

const decrementby5=counterBuilder(5); //we assign the function "decrement" to variable "decrementby5"

const decrementby3=counterBuilder(3); //we assign the function "decrement" to variable "decrementby3"

decrementby5() //95

decrementby5() //90

decrementby3() //97

decrementby3() //94

## **How can we add more functions as a decrement counter? Give an example of it**.

There are two ways to add more functions, shown in the following examples:

#### **First way to do it**:

function counter() {

  let counter = 0;
  
  function plus() {
  
    counter++;
    
    console.log(counter);
    
  }
  
  function minus() {
  
    counter--;
    
    console.log(counter);
    
  }
  
  return {
  
    increment: plus,
    
    decrement: minus
    
  }
  
}

const counters=counter() // we assign the return of the "counter" function to the variable "counters" 

console.log(counters) // { decrement: function minus() { counter--; console.log(counter); }, increment: function plus() { counter++; console.log(counter); } }

counters.decrement() //-1

counters.decrement() //-2

counters.increment() //-1

counters.increment() //0

counters.increment() //1

#### **Second way to do it**:

function counter() {

  let counter = 0;
  
  this.plus = () => {
  
    counter++;
    
    console.log(counter);
    
  }
  
  this.minus = () => {
  
    counter--;
    
    console.log(counter);
    
  }
  
}

const Counter = new counter(); // 

console.log(Counter) //{ minus: () => { counter--; console.log(counter); }, plus: () => { counter++; console.log(counter); } }

Counter.plus(); //11

Counter.plus(); //12

Counter.minus(); //11

Counter.minus(); //10

Counter.minus(); //9

## **What are the disadvantages of closures?**

- Variables used by closure will not be garbage collected.
- Memory snapshot of the application will be increased if closures are not used properly.
