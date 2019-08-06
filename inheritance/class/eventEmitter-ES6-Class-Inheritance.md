```javascript
/**
 * Demonstration of ES6 Class based Inheritance
 */

const { EventEmitter } = require('events');

class Person extends EventEmitter {
  constructor(name) {
    super();
    this.name = name;
  }
}

const benjaminFranklin = new Person('Benjamin Franklin');
benjaminFranklin.on('speak', function message(msg) {
  console.log(`${this.name} says ${msg}`);
});
benjaminFranklin.emit('speak', 'You may delay, but time will not');
```