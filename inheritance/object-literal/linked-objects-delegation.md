```javascript
/**
 * Demonstration of Inheritance (better called as Delegation) through Object-Linked-to-Other-Objects Delegation (OLOO)
 */

const Widget = {
  init(width, height) {
    this.id = null;
    this.width = width;
    this.height = height;
    this.element = null;
  },
  renderTo(parentContainer) {
    if (this.element) {
      this.element.style.width = `${this.width}px`;
      this.element.style.height = `${this.height}px`;
      parentContainer.appendChild(this.element);
    }
  },
  insertCustomStyle(style) {
    const newStyle = document.createElement('style');
    newStyle.innerHTML = style;
    const firstScriptTag = document.querySelector('script');
    firstScriptTag.parentNode.insertBefore(newStyle, firstScriptTag);
  }
};

const ButtonWidget = Object.create(Widget);

ButtonWidget.setup = function setup(id, width, height, label) {
  this.init(width, height);
  this.element = document.createElement('button');
  this.element.setAttribute('id', id);
  this.element.innerHTML = label;
  document.addEventListener('click', this.clickHandler);
};

ButtonWidget.clickHandler = function clickHandler(event) {
  console.log('clicked me', event.target.id);
};

ButtonWidget.build = function build(parentContainer) {
  this.renderTo(parentContainer);
  document.addEventListener('click', this.clickHandler);
};

/**
 * @example
 * How to use this button widget ?
 */
const parentContainer = document.getElementsByTagName('body')[0];
const b1 = Object.create(ButtonWidget);
b1.setup('b1', 100, 100, 'Widget 1');
const b2 = Object.create(ButtonWidget);
b2.setup('b2', 350, 100, 'Widget 2');
const b3 = Object.create(ButtonWidget);
b3.setup('b3', 100, 150, 'Widget 3');
b1.build(parentContainer);
b2.build(parentContainer);
b3.build(parentContainer);
b1.insertCustomStyle('body {background-color: #e5e5e5;} #b1 {background-color: #7FFF00;} ');
b2.insertCustomStyle('#b2 {background-color: #ff00c8;}');
b3.insertCustomStyle('#b3 {background-color: #00c4ff;}');
```