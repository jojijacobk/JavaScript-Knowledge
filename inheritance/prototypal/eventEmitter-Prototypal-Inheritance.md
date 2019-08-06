```javascript
/**
 * Demonstration of Prototypal Inheritance using javascript functions
 */

const { EventEmitter } = require('events');

function Person(name) {
  EventEmitter.call(this);
  this.name = name;
}
Person.prototype = Object.create(EventEmitter.prototype);

const benjaminFranklin = new Person('Benjamin Franklin');
benjaminFranklin.on('speak', function message(msg) {
  console.log(`${this.name} says ${msg}`);
});
benjaminFranklin.emit('speak', 'You may delay, but time will not');
```