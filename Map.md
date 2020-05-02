# Map
## Difference between Map and Object
Map is similar to Object but with a few more features.
1. Map can have keys of any type whereas Object can have only string keys. 
  Map can have a string, number, boolean or even an object as a key. But, Object would convert anything into a string as key. So for eg: 
  ```javascript
  //Demonstration of object key for an Object
  let john={
      name: 'john',
      id:1
  }

  let O1 = {};
  O1[john] = 100; 
  // the key john would become as {[object Object]: 100}

  // Demonstration of object key for a map
  let map = new Map();
  map.set(john,100);
  console.log(map.get(john)); // 100
```

2. Map iterates in the same order as how elements are inserted whereas for objects there is no order.

## Map methods

```javascript
let m1 = new Map();

m1.set(key,value);
m1.get(key)
m1.delete(key)
m1.has(key)
m1.clear()
m1.count
```
## Iterate a map
```javascript
1. keys()
for(let k of map.keys()) {

}

2. values()
for(let v of map.values()) {

}

3. entries()
for(let [k,v] of map.entries()) {

}

4. forEach()
map.forEach((value,key,map)=>{

});
```

## Convert an object to a map
```javascript
let fruits = {
    apple:1,
    banana:5,
    orange:3
};
let fruitsMap = new Map(Object.entries(fruits));
fruitsMap.get('banana'); // 5
```

## Convert a map to an object
```javascript
let fruitsMap = new Map([['apple',1],['banana',5],['orange',3]]);

let fruits = Object.fromEntries(fruitsMap.entries());
```