```javascript
/**
 * Demonstration of Prototypal Inheritance using javascript functions
 */

/**
 * Widget
 * @abstract
 * @param {number} width
 * @param {number} height
 */
function Widget(width, height) {
  this.id = null;
  this.width = width;
  this.height = height;
  this.element = null;
}
/**
 * Widget prototype method
 * @function renderTo
 */
Widget.prototype.renderTo = function renderTo(parentContainer) {
  if (this.element) {
    this.element.style.width = `${this.width}px`;
    this.element.style.height = `${this.height}px`;
    parentContainer.appendChild(this.element);
  }
};
/**
 * Widget prototype method
 * @function insertCustomStyle
 */
Widget.prototype.insertCustomStyle = function insertCustomStyle(style) {
  const newStyle = document.createElement('style');
  newStyle.innerHTML = style;
  const firstScriptTag = document.querySelector('script');
  firstScriptTag.parentNode.insertBefore(newStyle, firstScriptTag);
};

/**
 * This is the constructor function for ButtonWidget
 * @constructor
 * @param {string} id - A unique label as id for the element
 * @param {number} width - Width in pixels
 * @param {number} height - Height in pixels
 * @param {number} label - Label to identify a button widget
 */
function ButtonWidget(id, width, height, label) {
  Widget.call(this, width, height);
  this.element = document.createElement('button');
  this.element.setAttribute('id', id);
  this.element.innerHTML = label;
}

ButtonWidget.prototype = Object.create(Widget.prototype);

/**
 * ButtonWidget prototype method
 * @function clickHandler
 * @param {Object} event - click event
 */
ButtonWidget.prototype.clickHandler = function(event) {
  console.log('clicked me', event.target.id);
};

ButtonWidget.prototype.renderTo = function renderTo(parentContainer) {
  Widget.prototype.renderTo.call(this, parentContainer);
  document.addEventListener('click', this.clickHandler);
};

/**
 * @example
 * How to use this button widget ?
 */
const parentContainer = document.getElementsByTagName('body')[0];
const b1 = new ButtonWidget('b1', 100, 100, 'Widget 1');
const b2 = new ButtonWidget('b2', 350, 100, 'Widget 2');
const b3 = new ButtonWidget('b3', 100, 150, 'Widget 3');
b1.renderTo(parentContainer);
b2.renderTo(parentContainer);
b3.renderTo(parentContainer);
b1.insertCustomStyle('body {background-color: #e5e5e5;} #b1 {background-color: #7FFF00;} ');
b2.insertCustomStyle('#b2 {background-color: #ff00c8;}');
b3.insertCustomStyle('#b3 {background-color: #00c4ff;}');
```