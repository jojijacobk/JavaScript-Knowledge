   * [Objects](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#objects)
      * [Built in objects](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#built-in-objects)
      * [Primitive literals](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#primitive-literals)
      * [Contents of Object](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#contents-of-object)
      * [Arrays](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#arrays)
      * [Duplicating Objects](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#duplicating-objects)
      * [Property Descriptors](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#property-descriptors)
   * [Types](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#types)
   * [Inheritance](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#inheritance)
      * [Mixin](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#mixin)
         * [Explicit mixin ](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#explicit-mixin)
         * [Implicit mixin ](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#implicit-mixin)
      * [<strong>Javascript Prototype</strong>](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#javascript-prototype)
      * [Shadowing Properties](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#shadowing-properties)
      * [Prototype linkage](https://github.com/jojijacobk/About-Javascript/blob/master/Object-&-Prototype.md#prototype-linkage)

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

-   Object.defineProperty
-   Object.getOwnPropertyDescriptors
-   Immutability
    -   Object property as constant = Writable false + Configurable false
    -   Prevent Extensions
    -   Seal = Prevent Extensions + Configurable false
    -   Freeze = Prevent Extensions + Writable false
    -   Deep Freeze = Recursively (Prevent Extensions + Writable false)

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

-   6 Primary Types are there in javascript language   
    -   5 are primitives - string, number, boolean, null, undefined
        -   null - isn't object, its a bug
    -   6th is  Object
        -   sub types
            -   array (**structured contents** as compared to object)
            -   function (**callable object** - aka "first class"
                objects)

# Inheritance

-   Javascript doesn't offer Class based OO similar to other OO
    languages. Even the class syntax introduced in ES6 is just a
    syntactic sugar. 
-   Javascript do only have objects (and no classes per say).

## Mixin

You can circumvent the Prototypal Inheritance with Mixin

-   -   ### Explicit mixin 

        -   Extend

            In various popular libraries extend is a custom
            implementation to simply copy properties (including
            functions) from one object to another. **Note:** be aware
            that even though we copy properties(including functions) ,
            still the functions are shared references.

        -   Parasitic inheritance

             Another variation is called as  as termed by Doughlas
            Crockford. 

    -   ### Implicit mixin 

## **Javascript Prototype**

-   A.[[Prototype]] is the representation of an object A's prototype
-   Access prototype of an object
    -   `Object.getPrototype(A)`
    -   `Object.setPrototype(A , protoObject)`
    -   `Object.__proto__`
-   Prototypal inheritance
-   Property shadowing
-   Different levels of properties in a function
    -   Instance properties
    -   Prototype properties
    -   Static properties
-   Internals of constructor function (eg: new f())

## Shadowing Properties

When you set a property in an object, if that property doesn't exist
directly on that object, there are 3 scenarios reflecting how it works:

1.  If the property is not in the direct object, but present somewhere
    in prototype chain (in writable mode), then new property is set
    directly
2.  If the property is not in the direct object, but present somewhere
    in prototype chain in read only mode, then new property is
    discarded.
    1.  But this would work if you use property descriptors instead of
        assignment operator
3.  If the property is not in the direct object, but a setter is present
    in direct object, then new property is not set, but the setter is
    invoked.

## Prototype linkage

|Class oriented OO languages (PHP, Java etc)|Javascript|
|----------|-------|
|When you make an instance (lets say instance "a" from constructor "Foo"), <br/> `var a = new Foo();` <br/> object `a` copies characteristics of "Foo" into "a".| Every objects are linked to its `[[Prototype]]` object. So, when you make an instance (lets say instance "a" from constructor "Foo"), <br/> `var a = new Foo();` <br/> object `a` is not actually copying characteristics of "Foo" into "a" like in other OO languages. Instead instance "a" is `[[Prototype]] linked` to Foo.|
| So if 10 instance objects are made, 10 `copies` of FOO are made.|So if 10 instance objects are made, `10 [[Prototype]] linkages` to this common FOO object are made.|

-   `__proto__` is non standard way of getting/setting prototype of an object |
-   `Object.create(null) - best for dictionary```
-   Foo.prototype.isPrototypeOf(new Bar())
