# class-utils [![NPM version](https://badge.fury.io/js/class-utils.svg)](http://badge.fury.io/js/class-utils)

> Utils for working with JavaScript classes and prototype methods.

## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i class-utils --save
```

## Usage

```js
var cu = require('class-utils');
```

## API

### [.has](index.js#L37)

Returns true if an array has any of the given elements, or an object has any of the give keys.

**Params**

* `obj` **{Object}**
* `val` **{String|Array}**
* `returns` **{Boolean}**

**Example**

```js
cu.has(['a', 'b', 'c'], 'c');
//=> true

cu.has(['a', 'b', 'c'], ['c', 'z']);
//=> true

cu.has({a: 'b', c: 'd'}, ['c', 'z']);
//=> true
```

### [.hasAll](index.js#L84)

Returns true if an array or object has all of the given values.

**Params**

* `val` **{Object|Array}**
* `values` **{String|Array}**
* `returns` **{Boolean}**

**Example**

```js
cu.hasAll(['a', 'b', 'c'], 'c');
//=> true

cu.hasAll(['a', 'b', 'c'], ['c', 'z']);
//=> false

cu.hasAll({a: 'b', c: 'd'}, ['c', 'z']);
//=> false
```

### [.arrayify](index.js#L111)

Cast the given value to an array.

**Params**

* `val` **{String|Array}**
* `returns` **{Array}**

**Example**

```js
cu.arrayify('foo');
//=> ['foo']

cu.arrayify(['foo']);
//=> ['foo']
```

### [.hasConstructor](index.js#L146)

Returns true if a value has a `contructor`

**Params**

* `value` **{Object}**
* `returns` **{Boolean}**

**Example**

```js
cu.hasConstructor({});
//=> true

cu.hasConstructor(Object.create(null));
//=> false
```

### [.nativeKeys](index.js#L168)

Get the native `ownPropertyNames` from the constructor of the given `object`. An empty array is returned if the object does not have a constructor.

**Params**

* `obj` **{Object}**: Object that has a `constructor`.
* `returns` **{Array}**: Array of keys.

**Example**

```js
cu.nativeKeys({a: 'b', b: 'c', c: 'd'})
//=> ['a', 'b', 'c']

cu.nativeKeys(function(){})
//=> ['length', 'caller']
```

### [.getDescriptor](index.js#L200)

Returns property descriptor `key` if it's an "own" property of the given object.

**Params**

* `obj` **{Object}**
* `key` **{String}**
* `returns` **{Object}**: Returns descriptor `key`

**Example**

```js
function App() {}
Object.defineProperty(App.prototype, 'count', {
  get: function() {
    return Object.keys(this).length;
  }
});
cu.getDescriptor(App.prototype, 'count');
// returns:
// {
//   get: [Function],
//   set: undefined,
//   enumerable: false,
//   configurable: false
// }
```

### [.copyDescriptor](index.js#L230)

Copy a descriptor from one object to another.

**Params**

* `receiver` **{Object}**
* `provider` **{Object}**
* `name` **{String}**
* `returns` **{Object}**

**Example**

```js
function App() {}
Object.defineProperty(App.prototype, 'count', {
  get: function() {
    return Object.keys(this).length;
  }
});
var obj = {};
cu.copyDescriptor(obj, App.prototype, 'count');
```

### [.copy](index.js#L255)

Copy static properties, prototype properties, and descriptors
from one object to another.

**Params**

* `receiver` **{Object}**
* `provider` **{Object}**
* `omit` **{String|Array}**: One or more properties to omit
* `returns` **{Object}**

### [.inherit](index.js#L289)

Inherit the static properties, prototype properties, and descriptors
from of an object.

**Params**

* `receiver` **{Object}**
* `provider` **{Object}**
* `omit` **{String|Array}**: One or more properties to omit
* `returns` **{Object}**

### [.extend](index.js#L332)

Returns a function for extending the static properties, prototype properties, and descriptors from the `Parent` constructor onto `Child` constructors.

**Params**

* `Parent` **{Function}**: Parent ctor
* `Child` **{Function}**: Child ctor
* `proto` **{Object}**: Optionally pass additional prototype properties to inherit.
* `returns` **{Object}**

**Example**

```js
var extend = cu.extend(Parent);
Parent.extend(Child);

// optional methods
Parent.extend(Child, {
  foo: function() {},
  bar: function() {}
});
```

## Related projects

* [define-property](https://www.npmjs.com/package/define-property): Define a non-enumerable property on an object. | [homepage](https://github.com/jonschlinkert/define-property)
* [delegate-properties](https://www.npmjs.com/package/delegate-properties): Deep-clone properties from one object to another and make them non-enumerable, or make existing properties… [more](https://www.npmjs.com/package/delegate-properties) | [homepage](https://github.com/jonschlinkert/delegate-properties)
* [is-descriptor](https://www.npmjs.com/package/is-descriptor): Returns true if a value has the characteristics of a valid JavaScript descriptor. Works for… [more](https://www.npmjs.com/package/is-descriptor) | [homepage](https://github.com/jonschlinkert/is-descriptor)

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/class-utils/issues/new).

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2015 Jon Schlinkert
Released under the MIT license.

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on September 15, 2015._
