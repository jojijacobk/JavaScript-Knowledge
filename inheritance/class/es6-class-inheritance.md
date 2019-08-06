```javascript
/**
 * Demonstration of ES6 Class based Inheritance
 */

class Widget {
  constructor(width, height) {
    this.id = null;
    this.width = width;
    this.height = height;
    this.element = null;
  }

  renderTo(parentContainer) {
    if (this.element) {
      this.element.style.width = `${this.width}px`;
      this.element.style.height = `${this.height}px`;
      parentContainer.appendChild(this.element);
    }
  }

  insertCustomStyle(style) {
    const newStyle = document.createElement('style');
    newStyle.innerHTML = style;
    const firstScriptTag = document.querySelector('script');
    firstScriptTag.parentNode.insertBefore(newStyle, firstScriptTag);
  }
}

class ButtonWidget extends Widget {
  constructor(id, width, height, label) {
    super(width, height);
    this.element = document.createElement('button');
    this.element.setAttribute('id', id);
    this.element.innerHTML = label;
  }

  clickHandler(event) {
    console.log('clicked me', event.target.id);
  }

  renderTo(parentContainer) {
    super.renderTo(parentContainer);
    document.addEventListener('click', this.clickHandler);
  }
}

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