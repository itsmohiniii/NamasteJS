# Episode 9 : Block Scope & Shadowing in JS

What is a **Block**?
* Block aka *compound statement* is used to group multiple JS statements together into 1 group. We group them within {...}       
  Block wraps together multiple statements so that we can use it in a place where JS expects one statement.      
  Eg, Blocks are used in if statement, for loop, while loop etc.

    ```js
     //this is valid JS code 
    {
    } 
    ```
    
* Block Scope: what all variables and functions we can access inside this block is known as scope of the block.
    
    ```js
    {
        var a = 10;
        let b = 20;
        const c = 30;
        // Here let and const are hoisted in Block scope,
        // While, var is hoisted in Global scope.
    }
    ```

* Block Scope and its accessibility example
    ```js
    {
        var a = 10;
        let b = 20;
        const c = 30;
        console.log(a); // 10
        console.log(b); // 20
        console.log(c); // 30
    }
    console.log(a); // 10
    console.log(b); // Uncaught ReferenceError: b is not defined
    console.log(c); // Uncaught ReferenceError: c is not defined
    ```
    * Reason?
        * In the BLOCK SCOPE; we get b and c inside it initialized as *undefined* as a part of hoisting (reserved in a seperate memory space called **block**)
        * While, a is stored inside a GLOBAL scope. 

        * Thus we say, *let* and *const* are BLOCK SCOPED. They are stored in a separate memory space which is reserved for this block. Also, they can't be accessed outside this block. But var 'a' can be accessed anywhere as it is in global scope. Thus, we can't access them outside the Block.

What is **Shadowing**?

* ```js
    var a = 100; //stored in Global Memory space
    {
        var a = 10; // same name as global var //stored in Global Memory space (does not create a new variable, just updates the value)
        let b = 20; //stored in Block Memory space
        const c = 30; //stored in Block Memory space
        console.log(a); // 10
        console.log(b); // 20
        console.log(c); // 30 
    }
    console.log(a); // 10, instead of the 100 we were expecting. So block "a" modified val of global "a" as well. In console, only b and c are in block space. a initially is in global space(a = 100), and when a = 10 line is run, a is not created in block space, but replaces 100 with 10 in global space itself. 
    ```

* So, If one has same named variable outside the block, the variable inside the block *shadows* the outside variable. **This happens only for var**

* Let's observe the behaviour in case of let and const and understand it's reason.
    ```js
    let b = 100; //stored in Script Memory space
    {
        var a = 10; //stored in Global Memory space
        let b = 20; //stored in Block Memory space
        const c = 30; //stored in Block Memory space
        console.log(b); // 20
    }
    console.log(b); // 100, Both b's are in separate spaces (one in Block(20) and one in Script(another arbitrary mem space)(100)). Same is also true for *const* declarations.
    ```
    ![Block Scope Explaination](/assets/scope.jpg "Lexical Scope")


* Same logic is true even for **functions**
    ```js
    const c = 100; //stored in Script Memory space
    function x() {
        const c = 10; //stored in Local Memory space
        console.log(c); // 10
    }
    x();
    console.log(c); // 100
    ```

    ```js
    var c = 100; //stored in Global Memory space
    function x() {
        var c = 10; //stored in Local Memory space
        console.log(c); // 10
    }
    x();
    console.log(c); // 100
    ```

What is **Illegal Shadowing**?

* ```js
    let a = 20;
    {
        var a = 20; //Illegal shadowing (We cannot shadow let with var)
    }
    // Uncaught SyntaxError: Identifier 'a' has already been declared
    // It throws an error because in a particular scope, let can't be redeclared.
    ```
  
    ```js
    var a = 20;
    {
        var a = 20; // Valid (we can shadow var using a var)
    }
    ```

    ```js
    let a = 20;
    {
        let a = 20; // Valid (we can shadow let using let)
    }
    ```
    
    ```js
    var a = 20;
    {
        let a = 20; // Valid (we can shadow var using let)
    }
    ```
    
    * We cannot shadow let with var. But it is **valid** to shadow a let using a let. However, we can shadow var with let.
    * All scope rules that work in function are same in arrow functions too.
    * Since var is function scoped, it is not a problem with the code below.
        ```js
        let a = 20;
        function x() {
            var a = 20;
        }
        ```
  * var is function scoped. (Global, Local)
  * let and const are block-scoped. (Script, Block, Local)
 
  * Block scope also follows lexical scope and lexical scope chain pattern.    
    Lexical scope works the same way inside the block also.
     
    ```js
    const a = 20; //Script mem space
    {
        const a = 100; //Block mem space
        {
            const a = 200; //it has its own Block Mem space
            console.log(a); //200
        }
        console.log(a); //100
    }
     console.log(a); //20
    ```

    ```js
    const a = 20; //Script mem space
    {
        const a = 100; //Block mem space
        {
            console.log(a); //100
        }
    }
    ```
    




<hr>

Watch Live On Youtube below:

<a href="https://www.youtube.com/watch?v=lW_erSjyMeM&ab_channel=AkshaySaini" target="_blank"><img src="https://img.youtube.com/vi/lW_erSjyMeM/0.jpg" width="750"
alt="Block Scope & Shadowing in JS Youtube Link"/></a>
