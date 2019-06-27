  * [What is this in JavaScript?](Deep-Dive-Into-"this"-Operator.md#what-is-this-in-JavaScript)
      * [Common misconceptions about <em>this</em>](Deep-Dive-Into-"this"-Operator.md#common-misconceptions-about-this)
      * [What are the possible alternatives to avoid usage of <em>this</em>](Deep-Dive-Into-"this"-Operator.md#what-are-the-possible-alternatives-to-avoid-usage-of-this)
      * [How to embrace usage of this](Deep-Dive-Into-"this"-Operator.md#how-to-embrace-usage-of-this)
      * [How to determine the context of <em>this</em> by inspecting call site](Deep-Dive-Into-"this"-Operator.md#how-to-determine-the-context-ofthis-by-inspecting-call-site)
         * [1. Default binding](Deep-Dive-Into-"this"-Operator.md#1default-binding)
            * [Default binding under strict mode](Deep-Dive-Into-"this"-Operator.md#default-binding-under-strict-mode)
         * [2. Implicit binding](Deep-Dive-Into-"this"-Operator.md#2-implicit-binding)
            * [Implicitly Lost](Deep-Dive-Into-"this"-Operator.md#implicitly-lost)
            * [Aliasing](Deep-Dive-Into-"this"-Operator.md#aliasing)
            * [callback](Deep-Dive-Into-"this"-Operator.md#callback)
         * [3. Explicit binding](Deep-Dive-Into-"this"-Operator.md#3-explicit-binding)
            * [apply](Deep-Dive-Into-"this"-Operator.md#apply)
            * [call](Deep-Dive-Into-"this"-Operator.md#call)
            * [bind](Deep-Dive-Into-"this"-Operator.md#bind)
            * [Bind alternatives](Deep-Dive-Into-"this"-Operator.md#bind-alternatives)
         * [4. new Operator](Deep-Dive-Into-"this"-Operator.md#4-new-operator)
         * [5. Lexical this](Deep-Dive-Into-"this"-Operator.md#5-lexical-this)
         * [Precedence order of rules](Deep-Dive-Into-"this"-Operator.md#precedence-order-of-rules)
      * [Binding Exceptions](Deep-Dive-Into-"this"-Operator.md#binding-exceptions)
         * [Ignored this](Deep-Dive-Into-"this"-Operator.md#ignored-this)
         * [Safer this](Deep-Dive-Into-"this"-Operator.md#safer-this)

# What is `this` in JavaScript?

*`this`* keyword is a special identifier which is automatically defined
in the scope of every JavaScript functions. `this` is not an author time
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

`this` usage makes JavaScript functions cleaner APIs. You could embrace
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

