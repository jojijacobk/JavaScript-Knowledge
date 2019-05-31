   * [What is this in Javascript?](README.md#what-is-this-in-javascript)
      * [Common misconceptions about <em>this</em>](README.md#common-misconceptions-about-this)
      * [What are the possible alternatives to avoid usage of <em>this</em>](README.md#what-are-the-possible-alternatives-to-avoid-usage-of-this)
      * [How to embrace usage of this](README.md#how-to-embrace-usage-of-this)
      * [How to determine the context of <em>this</em> by inspecting <strong>call site</strong>](README.md#how-to-determine-the-context-ofthis-by-inspecting-call-site)
         * [1. Default binding](README.md#1default-binding)
            * [<strong>Default binding under strict mode</strong>](README.md#default-binding-under-strict-mode)
         * [2. Implicit binding](README.md#2-implicit-binding)
            * [<strong>Implicitly Lost</strong>](README.md#implicitly-lost)
            * [<strong>Aliasing</strong>](README.md#aliasing)
            * [<strong>callback</strong>](README.md#callback)
         * [3. Explicit binding](README.md#3-explicit-binding)
            * [apply](README.md#apply)
            * [call](README.md#call)
            * [bind](README.md#bind)
            * [Bind alternatives](README.md#bind-alternatives)
         * [4. new Operator](README.md#4-new-operator)
         * [5. Lexical this](README.md#5-lexical-this)
         * [Precedence order of rules](README.md#precedence-order-of-rules)
      * [Binding Exceptions](README.md#binding-exceptions)
         * [<strong>Ignored this</strong>](README.md#ignored-this)
         * [<strong>Safer this</strong>](README.md#safer-this)
   * [Objects](README.md#objects)
      * [Built in objects](README.md#built-in-objects)
      * [Primitive literals](README.md#primitive-literals)
      * [Contents of Object](README.md#contents-of-object)
      * [Arrays](README.md#arrays)
      * [Duplicating Objects](README.md#duplicating-objects)
      * [Property Descriptors](README.md#property-descriptors)
   * [Types](README.md#types)
   * [Inheritance](README.md#inheritance)
      * [Mixin](README.md#mixin)
         * [Explicit mixin ](README.md#explicit-mixin)
         * [Implicit mixin ](README.md#implicit-mixin)
      * [<strong>Javascript Prototype</strong>](README.md#javascript-prototype)
      * [Shadowing Properties](README.md#shadowing-properties)
      * [Prototype linkage](README.md#prototype-linkage)

# What is `this` in Javascript?

*`this`* keyword is a special identifier which is automatically defined
in the scope of every javascript functions. `this` is not an author time
binding but a run time binding depending on the call site from where the
function is being invoked. 

## Common misconceptions about *`this`*

1.  **misconception-1:** *`this`* refers to the function itself.
2.  **misconception-2:** *`this`* refers to the lexical scope where it
    is being used.

## What are the possible alternatives to avoid usage of *`this`*

You have different workarounds from using *`this`* at all.

1.  call the current function by its name other than by *`this`*
    1.  **cons:** by hardcoding function name inside the function you
        lose reusability
2.  pass any data or context object as parameters to function so that
    you don't ever need to call `this` inside a function to point to
    properties.
    1.  **cons:** by passing params it becomes messier

## How to embrace usage of `this`

`this` usage makes javascript functions cleaner APIs. You could embrace
its usage by:

1.  learn how to properly use `this`
2.  enforce `this` to point to the current function object (by call,
    apply or bind) 

## How to determine the context of *`this`* by inspecting **call site**

When you see *this *in a function, in order to understand to what
context is *this* related to, you just need to scan through the call
stack to reach the call site of that function's invocation, and inspect
for the following 4 rules.

The 4 Rules :

### 1. Default binding

If a function is called plain and undecorated, then it goes to the
default binding, where the *`global object`* is bound as *this* context.

#### **Default binding under strict mode**

But, if your function executes in strict
mode, then global object will not be available for binding. So,
*this* context will be `undefined`.

### 2. Implicit binding

If the function is owned/contained by another object, then *this* is
bound to that container object.

#### **Implicitly Lost**

Implicit binding doesn't work in certain situations such as :

-   -   #### **Aliasing**

        In cases like `var bar = Obj.foo`, here the `Obj.foo` is aliased
        as *`bar`*. And, so implicit binding is lost as `bar` would
        simply gets executed as plain function invocation.

    -   #### **callback**

        In cases like *`Obj.foo`* is passed as an argument (aka
        callback), it is like alias referencing and loses implicit
        binding.

### 3. Explicit binding

To avoid the case of losing binding or unexpected binding, you can force
the binding with **hard binding**. It can be achieved using any of the
following.

- #### apply
- #### call
- #### bind

#### Bind alternatives
- **`self = this`** technique
- ES6 **arrow function**

### 4. new Operator

When you instantiate a new object by prefixing `new` operator with a
function call, then `this` refers to the new object.

### 5. Lexical this

ES6 introduced **Arrow functions** which supersedes all the 4 rules
above in capturing lexical scope of enclosed function into *this*
context.

### Precedence order of rules

`arrow function` > `new` > `explicit` > `implicit` > `default`

## Binding Exceptions

- ### **Ignored this**

    You may call some functions with an explicit binding
    to `null` or `undefined` expecting to ignore this at all. But,
    sometimes it may happen to fall into default binding
    of `global` object. Consequently your global object may get mutated
    if its a third party library. 

-   ### **Safer this**

    To avoid this case you can hard bind to an **empty object** (aka
    DMZ - Demilitarised Zone) : **`var DMZ = Object.create(null)`**

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
