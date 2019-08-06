```javascript
/**
 * Demonstration of Inheritance (better called as Delegation) through Object-Linked-to-Other-Objects Delegation (OLOO)
 */

const { EventEmitter } = require('events');

const person = Object.create(EventEmitter.prototype);
person.name = null;

const benjaminFranklin = Object.create(person);
benjaminFranklin.on('speak', function message(msg) {
  console.log(`${this.name} says ${msg}`);
});
benjaminFranklin.emit('speak', 'You may delay, but time will not');
```