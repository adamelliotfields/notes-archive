# ImmutableJS Cheatsheet
> :calendar: *June 12, 2017*

This is a running list of Immutable.js snippets and tips that I've used (and will probably use again).

### Update an item in a Collection

```javascript
const list = List([1, 2, 3, 4]);
const map = Map({ key: 'value' });

list.update(0, item => 2); // List([2, 2, 3, 4])
map.update('key', value => 'new value'); // Map({ key: 'new value' })
```

### Get the length of a Collection
*Hint: It's not `length`!*  

```javascript
const list = List([1, 2, 3, 4]);
const map = Map({ key: 'value' });

// Lazy evaluation
list.size; // 4
map.size; // 1

// Non-lazy evaluation
list.count(); // 4
map.count(); // 1
```

### Get the count of a Collection based on a Predicate

```javascript
const range = Range(1, 11); // Range([1...10])

range.count(item => item % 2 === 0); // 5
```

### Empty a Collection

```javascript
const list = List([1, 2, 3, 4]);
const map = Map({ key: 'value' });

list.clear(); // List([])
map.clear(); // Map({})
```

### Reverse filter a Collection

```javascript
const range = Range(1, 11);
const map = Map({ a: 0, b: 1 });

range.filterNot(item => item % 2 === 0); // Seq([1, 3, 5, 7, 9])
map.filterNot(value => value > 0); // Map({ a: 0 })
```

### Group a Collection based on a Predicate

```javascript
const list = List([1, 2, 3, 4]);
const map = Map({ a: 0, b: 1 });

list.groupBy(item => item % 2 === 0); // OrderedMap({ false: [1, 3], true: [2, 4] })
map.groupBy(value => value > 0); // Map({ false: { a: 0 }, true: { b: 1} })
```

### Flip the keys and values of a Map

```javascript
const map = Map({ a: 0, b: 1 });

map.flip(); // Map({ 0: 'a', 1: 'b' })
```

### Get the index of a Map in a List

```javascript
const cars = List.of(
  Map({ make: 'BMW', model: 'M3' }),
  Map({ make: 'Audi', model: 'RS4' })
);

cars.findIndex((car) => car.get('model') === 'RS4'); // 1
```

### Get a List of items based on amount

```javascript
const list = List([1, 2, 3, 4]);

list.take(2); // List([1, 2])

list.takeLast(2); // List([3, 4])
```

### Update a Map in a List

```javascript
const cars = List.of(
  Map({ make: 'BMW', model: 'M3' }),
  Map({ make: 'Audi', model: 'RS4' })
);

// Get the index (resist the urge for a one-liner)
const rs4 = cars.findIndex(car => car.get('model') === 'RS4');

// Update the Map at the specified index
cars.update(rs4, car => car.update('model', model => 'RS7'));
```

### Filter a List of Maps

```javascript
const cars = List.of(
  Map({ make: 'BMW', model: 'M3' }),
  Map({ make: 'Audi', model: 'RS4' })
);

cars.filter(car => car.get('make') === 'BMW');
```

### Test all values in a List and return a boolean

```javascript
const todos = List.of(
  Map({ id: 1, title: 'Write a Gist', completed: true }),
  Map({ id: 2, title: 'Start next React project', completed: false })
);

// List.some() returns true if ANY value is truthy
todos.some(todo => todo.get('completed')); // true

//List.every() returns true only if ALL values are truthy
todos.every(todo => todo.get('completed')); // false
```

### Convert a List to an Ordered Map

```javascript
const list = List([1, 2, 3, 4]);

list.toOrderedMap(); // OrderedMap({ 0: 1, 1: 2, 2: 3, 3: 4 })
```

### Convert a List of Maps to a List

```javascript
const cars = List.of(
  Map({ make: 'BMW', model: 'M3' }),
  Map({ make: 'Audi', model: 'RS4' })
);

cars.flatten(); // List(['BMW', 'M3', 'Audi', 'RS4'])
```

### Get a Map in a List based on a Predicate

```javascript
const cars = List.of(
  Map({ make: 'BMW', model: 'M3' }),
  Map({ make: 'Audi', model: 'RS4' })
);

cars.find(car => car.get('model') === 'M3'); // Map({ make: 'BMW', model: 'M3' })
```

### Toggle the value of a Map in a List

```javascript
const todos = List.of(
  Map({ id: 1, title: 'Write a Gist', completed: false})
);

const index = todos.findIndex(todo => todo.get('id') === 1);

todos.update(index, todo => todo.update('completed', completed => !completed));
```

### Toggle all values in a List of Maps

```javascript
const todos = List.of(
  Map({ id: 1, title: 'Write a Gist', completed: false }),
  Map({ id: 2, title: 'Start next React project', completed: false })
);

// Use List.map() not List.update()
todos.map(todo => todo.update('completed', completed => true));
```

### Generate a Sequence of numbers

```javascript
const range = Range(1, 11); // Seq([1...10])

Seq.isSeq(range); // true
```
