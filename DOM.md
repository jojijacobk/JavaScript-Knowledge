# Browser environment

<img src="attachments/javascript in browser host environment.png" width="600px"> <br/>

DOM is not only for browsers. A server program can walk through DOM.

# Document Object Model

## DOM Tree

- Anything in HTML is represented in it's DOM Tree, which includes even the whitespace, newlines and comments along wiht the tags.
- The DOM tree of a web page starts with root element as `document`. It has two `childNodes` in general:

  - 1. `<!DOCTYPE html>` the doctype
  - 2. `<html>` the entire html

    <img src="attachments/childNodes of document.png" width="230px"> <br/>

- There are 12 types of nodes in a DOM Tree (doctype, document, element, attribute, text, comment etc)

**Text node**

- Whitespace anywhere inside a `<head>` tag and `<body>` tag is represented as `text` nodes in DOM. And, the whitespace between `<head>` tag and `<body>` tag is also represented as `text` node in DOM. Other whitespaces are ignored.
- The text inside an element is also represented as `text` node.
- So the text node is just a string, which has no children, and is always the leaf node of a DOM tree.

## DOM Traversal

- You can traverse through the DOM in two ways.

| Walk over all types of Nodes (including whitespace, comment, element etc) | Walk over only element Nodes                                             |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| <img src="attachments/Traversal through DOM nodes.png" width="500px">     | <img src="attachments/Traversal through DOM elements.png" width="600px"> |

**Note:**
`document.body.firstChild` may not be your first tag element inside HTML body. It could be a whitespace `text` node if your HTML is formatted with spaces like a normal page. But, `document.body.firstElementChild` is always gonna be the first **tag** element.

<img src="attachments/difference between node and element 2.png" width="300px"> <br/>
<img src="attachments/difference between node and element 1.png" width="500px"> <br/>

- To iterate the nodes collection returned by DOM methods, you can try any of the following:

  - `for..of` iteration on collection
  - `for..in` iteration on collection with `hasOwnProperty` check
  - ordinary `for()` loop iteration on collection
  - convert collection into array and iterate using array methods like: `Array.from`(collection).forEach()

## Search inside DOM

<img src="attachments/different ways to search element.png" width="700px"> <br/>\
<img src="attachments/matches, closest, contains .png" width="700px"> <br/>

## DOM node classes

The properties and methods present in a `tag` are inherited from a hierarchy of different classes.
For example, for an anchor tag

- anchor tag specific attributes such as `href` are inherited from `HTMLAnchorElement` class
- common html attributes are inherited from `HTMLElement` class
- `nextElementSibling` property inherited from `Element` class
- `nextSibling` property inherited from `Node` class
- `events` are attributed from `EventTarget` class

<img src="attachments/DOM node classes.png" width="500px"> <br/>

A node object is like a regular JavaScript object. So, you can add new properties and methods to it.

You can use `console.log(element)` to explore the **HTML** representing that element,
whereas `console.dir(element)` to display the **object** representing that element.

## Node

- `nodeType`
  <br> <img src="attachments/nodeType.png" width="500px"> <br>
- `nodeValue` / `data` - is used to get content of a nodes (other than element type)
- `nodeName` - is used to get the name of "any nodes" (including element nodes)
- `tagName` - is used to get only the name of "element nodes"
- `innerHTML` - is used to get/set **HTML** content of an element (valide only for element nodes)
- `textContent` - is used to get/set **text** content of an element (all HTML tags are stripped off during get, written as text during set)
- `outerHTML`

## Attributes

You can access the attributes of an element using it's object model like `inputElem.value`. But, some attributes exist only on certain type of nodes. Also, using object model you cannot access custom attributes you added to an element. So, there is a better way to access any attributes.

- `elem.hasAttribute(name)`
- `elem.getAttribute(name)` returns string value of that attribute
- `elem.setAttribute(name,value)`
- `elem.removeAttribute(name)`
- `elem.attributes` - get collection of all attributes as **attribute objects** that inherits from `Attr` class. Then you can call `attrObj.name`, `attrObj.value` to get attribute details.

Attributes are case-insensitive. But, other DOM properties in an element object are case sensitive.

When a user types some `input` element's value, that new value is updated in the DOM object property. But, that will not be updated in attribute. So, attribute always sticks to the value which was present in the HTML. Changes to that can be tracked from object property whereas original value can be tracked from attribute itself.

## Custom Attributes

You can mark any custom value to an element using classes. But, they are least elegant for this use case. Better approach is to use custom attributes. But, there is a catch that as HTML is a living standard, they might introduce an attribute similar to your own custom attribute. To avoid that conflict you can use `data-*` attribute. Any custom attributes you add with prefix `data-` will not conflict as they are reserved for programmers. And, such values are also accessible via `elem.dataset` property.

```
//HTML
<body data-hobby="cycling">

//JavaScript
document.body.dataset.hobby // cycling

//CSS
body[data-hobby] {
    color:red;
}
```

```
//HTML
<body data-professional-hobby="cycling">

//JavaScript
document.body.dataset.professionalHobby // cycling

//CSS
body[data-professional-hobby] {
    color:red;
}
```

## Modifying DOM

<img src="attachments/modify document.png" width="750px"> <br/>
