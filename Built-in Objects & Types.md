[toc]

# Objects

Objects can be created in two ways :

-   **object literal** syntax. 
    -   Adv: add numerous properties at once.
-   constructed **new Object()** form.

## Built in objects

1.  String
2.  Number
3.  Boolean
4.  Function
5.  Array
6.  Object
7.  Date
8.  RegExp
9.  Error 

## Primitive literals

They are coerced into object wrapper by JS engine when necessary. so it
is preferred than built in objects.

-   String, Number, Boolean are those
-   null & undefined have **NO object wrapper** form
-   Date has only constructor object form
-   Object, Array, Function, RegExp are all objects regardless of
    whether made via literal form or constructor form

## Contents of Object

-   **property names are always string**. if you put anything else, that
    is coerced to string
-   **access via dot** - (aka property access) - limitation to naming as
    compatible identifier
-   **access via `["name"]`** - (aka key access) - anything unicode
    supported
-   **computed property names** introduced in ES6 even for Object
    literal expression
-   ES 6 Symbols can be used as a computed name

## Arrays

-   Adding properties to Array object doesn't increase size of array
    because it only adds property to array object, and not to array
    container
-   Arrays are **good for numerically indexed contents** whereas objects
    are good for key-value store, where value can be objects or its sub
    types

## Duplicating Objects

-   To do shallow clone of an object, all you need to do is **ensure that an object is JSON safe**  
    `var clone= JSON.parse(JSON.stringify(obj))`
    OR  
    `var clone = Object.assign( {},obj1, obj2 ...)`

## Property Descriptors

https://javascript.info/property-descriptors

-   Object.defineProperty
-   Object.defineProperties
-   Object.getOwnPropertyDescriptors
-   Object.preventExtensions
-   Object.seal
-   Object.freeze
-   Object.isExtensible
-   Object.isSealed
-   Object.isFrozen

-   Getter & Setter
    -   If you try to access a non existent property in an object, it
        shows undefined. Whereas if you try to access a non existent
        variable, it shows ReferenceError: is not defined
    -   Existence check
        -   in operator. eg: ("a" in myObj); Dive deep into prototype
            chain
        -   hasOwnProperty check. DOESN'T Dive into prototype chain
    -   Enumeration
        -   for(var i in Obj) - loop through enumerable keys
        -   for(var v of Obj) - loop through values
        -   forEach(myObject) - loop through each item, and pass value
            into a callback function, never mind about return value of
            callback
        -   every(myObject)   - loop through each item, and pass value
            into a callback function, breaks when return value of
            callback is falsy
        -   some(myObject)    - loop through each item, and pass value
            into a callback function, breaks when return value of
            callback is truthy
        -   Object.keys() → gets enumerable keys
        -   myObject.propertyIsEnumerable("x") 
        -   If Array is just numerically indexed, it is good to have
            traditional iteration based on length
        -   If you want to enumerate an Object, you can go with for(var
            i in myObject) style iteration

# Types

-   6 Primary Types are there in JavaScript language   
    -   5 are primitives - string, number, boolean, null, undefined
        -   null - isn't object, its a bug
    -   6th is  Object
        -   sub types
            -   array (**structured contents** as compared to object)
            -   function (**callable object** - aka "first class"
                objects)

**Number**

-   In JavaScript, numbers are represented using Number data type. 
-   A number is 64 bit floating point representation of a number.
    -   1 bit for sign
    -   11 bits for exponents
    -   52 bits for the integer part of number

<img src="/Users/jojijaco/Oracle/VMShared/Projects/github/JavaScript/attachments/1187389524.png" width="550"/><br/>

-   The way floating point data types handle fractions is different than
    human calculation because they represent a fraction in binary form
    where there is no exact equivalent for some fraction values.   
    So, for eg: `.2 + .1` is not `.3`, but `0.30000000000000004`  
    To fix this issue you can use `.toFixed()`  
    like `(0.2+0.1).toFixed(1)`  
-   The highest possible integer value that can be handled by a Number
    type in JavaScript is `Number.MAX_SAFE_INTEGER`. Similarly,
    `Number.MIN_SAFE_INTEGER`
-   If you are going to work on high precision math, make use of some
    libraries which purely serve this purpose.

**Short-circuit evaluation**

-   `x || y` **fallback** to `y` if `x` is falsy
-   `x && y`  **pick** the last value if all `x, y` are truthy
-   right side part is evaluated only if necessary

**Bindings/Variables**

-   name of a binding 
    -   can start with **alphabets, _ , $**
    -   **can't** start with number or any other symbols
    -   **can't** be a reserved word