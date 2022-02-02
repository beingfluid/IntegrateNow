## Chapter 2
# Working with JSON


- JavaScript Object Notation (JSON) is a lightweight data-interchange format. 
- It is easy for humans to read and write. 
- It is easy for machines to parse and generate.
\

- Though many programming languages support JSON, it is especially useful for JavaScript-based apps, including websites and browser extensions.
\

- JSON is a syntax for serializing objects, arrays, numbers, strings, booleans, and null. 
- JSON can represent numbers, booleans, strings, null, arrays (ordered sequences of values), and objects (string-value mappings) made up of these values (or of other arrays and objects).  
\

It is based upon JavaScript syntax but is distinct from it: some JavaScript is not JSON.
- Property names must be double-quoted strings; trailing commas are forbidden.
- Leading zeros are prohibited. A decimal point must be followed by at least one digit. NaN and Infinity are unsupported.
- JSON does not natively represent more complex data types like functions, regular expressions, dates, and so on.
- Other differences include allowing only double-quoted strings and having no provisions for undefined or comments. 
- For those who wish to use a more human-friendly configuration format based on JSON, there is JSON5, used by the Babel compiler, and the more commonly used YAML.
\

### JSON object
- The JSON object contains methods for parsing JavaScript Object Notation (JSON) and converting values to JSON. 
- It can't be called or constructed, and aside from its two method properties, it has no interesting functionality of its own.
\

- Insignificant whitespace may be present anywhere except within a JSONNumber (numbers must contain no whitespace) or JSONString (where it is interpreted as the corresponding character in the string, or would cause an error). 
- The tab character (U+0009), carriage return (U+000D), line feed (U+000A), and space (U+0020) characters are the only valid whitespace characters.
\

### Example
```json
{
  "browsers": {
    "firefox": {
      "name": "Firefox",
      "pref_url": "about:config",
      "releases": {
        "1": {
          "release_date": "2004-11-09",
          "status": "retired",
          "engine": "Gecko",
          "engine_version": "1.7"
        }
      }
    }
  }
}
```

### Static methods
#### JSON.parse(text[, reviver])
- Parse the string text as JSON, optionally transform the produced value and its properties, and return the value. 
- Any violations of the JSON syntax, including those pertaining to the differences between JavaScript and JSON, cause a SyntaxError to be thrown.
- The reviver option allows for interpreting what the replacer has used to stand in for other datatypes.
\
- The JSON.parse() method parses a JSON string, constructing the JavaScript value or object described by the string. 
- An optional reviver function can be provided to perform a transformation on the resulting object before it is returned.
\
##### Syntax
```js
JSON.parse(text)
JSON.parse(text, reviver)
```

##### Parameters
###### text
The string to parse as JSON. See the JSON object for a description of JSON syntax.
```js
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
// expected output: 42

console.log(obj.result);
// expected output: true
```

###### reviver Optional (Using the reviver parameter)
- If a function, this prescribes how the value originally produced by parsing is transformed, before being returned.
- If a reviver is specified, the value computed by parsing is transformed before being returned. 
- Specifically, the computed value and all its properties (beginning with the most nested properties and proceeding to the original value itself) are individually run through the reviver. 
- Then it is called, with the object containing the property being processed as this, and with the property name as a string, and the property value as arguments. 
- If the reviver function returns undefined (or returns no value, for example, if execution falls off the end of the function), the property is deleted from the object. 
- Otherwise, the property is redefined to be the return value.
\
- If the reviver only transforms some values and not others, be certain to return all untransformed values as-is, otherwise, they will be deleted from the resulting object.
\
```js
JSON.parse('{"p": 5}', (key, value) =>
  typeof value === 'number'
    ? value * 2 // return value * 2 for numbers
    : value     // return everything else unchanged
);

// { p: 10 }

JSON.parse('{"1": 1, "2": 2, "3": {"4": 4, "5": {"6": 6}}}', (key, value) => {
  console.log(key); // log the current property name, the last is "".
  return value;     // return the unchanged property value.
});

// 1
// 2
// 4
// 6
// 5
// 3
// ""
```

###### Return value
The Object, Array, string, number, boolean, or null value corresponding to the given JSON text.
```js
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null
```

###### Exceptions
- Throws a SyntaxError exception if the string to parse is not valid JSON.
\
- JSON.parse() does not allow trailing commas
```js
// both will throw a SyntaxError
JSON.parse('[1, 2, 3, 4, ]');
JSON.parse('{"foo" : 1, }');
```
\
- JSON.parse() does not allow single quotes
```js
// will throw a SyntaxError
JSON.parse("{'foo': 1}");
```





#### JSON.stringify(value[, replacer[, space]])
- Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner. 
- By default, all instances of undefined are replaced with null, and other unsupported native data types are censored. 
- The replacer option allows for specifying other behavior.
\
- The JSON.stringify() method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.
\
##### Syntax
```js
JSON.stringify(value)
JSON.stringify(value, replacer)
JSON.stringify(value, replacer, space)
```
##### Parameters
###### value
The value to convert to a JSON string.
```js
console.log(JSON.stringify({ x: 5, y: 6 }));
// expected output: "{"x":5,"y":6}"

console.log(JSON.stringify([new Number(3), new String('false'), new Boolean(false)]));
// expected output: "[3,"false",false]"

console.log(JSON.stringify({ x: [10, undefined, function(){}, Symbol('')] }));
// expected output: "{"x":[10,null,null,null]}"

console.log(JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)));
// expected output: ""2006-01-02T15:04:05.000Z""

```

###### replacer Optional
- A function that alters the behavior of the stringification process, or an array of String and Number that serve as an allowlist for selecting/filtering the properties of the value object to be included in the JSON string. 
- If this value is null or not provided, all properties of the object are included in the resulting JSON string.

###### space Optional (The space argument)
- A String or Number object that's used to insert white space (including indentation, line break characters, etc.) into the output JSON string for readability purposes.
- If this parameter is not provided (or is null), no white space is used.
\
- If this is a Number, it indicates the number of space characters to use as white space for indenting purposes; this number is capped at 10 (if it is greater, the value is just 10). 
- Values less than 1 indicate that no space should be used.
\
- If this is a String, the string (or the first 10 characters of the string, if it's longer than that) is used as white space.
\
The space argument may be used to control spacing in the final string.

- If it is a number, successive levels in the stringification will each be indented by this many space characters (up to 10).
- If it is a string, successive levels will be indented by this string (or the first ten characters of it).

```js
JSON.stringify({ uno: 1, dos: 2 }, null, '\t');
// returns the string:
// '{
//     "uno": 1,
//     "dos": 2
// }'
```

##### Return value
A JSON string representing the given value, or undefined.

##### Description
JSON.stringify() converts a value to JSON notation representing it:

- If the value has a toJSON() method, it's responsible to define what data will be serialized.
- Boolean, Number, and String objects are converted to the corresponding primitive values during stringification, in accord with the traditional conversion semantics.
- undefined, Functions, and Symbols are not valid JSON values. If any such values are encountered during conversion they are either omitted (when found in an object) or changed to null (when found in an array). JSON.stringify() can return undefined when passing in "pure" values like JSON.stringify(function() {}) or JSON.stringify(undefined).
- All Symbol-keyed properties will be completely ignored, even when using the replacer function.
- The instances of Date implement the toJSON() function by returning a string (the same as date.toISOString()). Thus, they are treated as strings.
- The numbers Infinity and NaN, as well as the value null, are all considered null.
- All the other Object instances (including Map, Set, WeakMap, and WeakSet) will have only their enumerable properties serialized.


```js
JSON.stringify({});                    // '{}'
JSON.stringify(true);                  // 'true'
JSON.stringify('foo');                 // '"foo"'
JSON.stringify([1, 'false', false]);   // '[1,"false",false]'
JSON.stringify([NaN, null, Infinity]); // '[null,null,null]'
JSON.stringify({ x: 5 });              // '{"x":5}'

JSON.stringify(new Date(2006, 0, 2, 15, 4, 5));
// '"2006-01-02T15:04:05.000Z"'

JSON.stringify({ x: 5, y: 6 });
// '{"x":5,"y":6}'
JSON.stringify([new Number(3), new String('false'), new Boolean(false)]);
// '[3,"false",false]'

// String-keyed array elements are not enumerable and make no sense in JSON
let a = ['foo', 'bar'];
a['baz'] = 'quux';      // a: [ 0: 'foo', 1: 'bar', baz: 'quux' ]
JSON.stringify(a);
// '["foo","bar"]'

JSON.stringify({ x: [10, undefined, function() {}, Symbol('')] });
// '{"x":[10,null,null,null]}'

// Standard data structures
JSON.stringify([new Set([1]), new Map([[1, 2]]), new WeakSet([{a: 1}]), new WeakMap([[{a: 1}, 2]])]);
// '[{},{},{},{}]'

// TypedArray
JSON.stringify([new Int8Array([1]), new Int16Array([1]), new Int32Array([1])]);
// '[{"0":1},{"0":1},{"0":1}]'
JSON.stringify([new Uint8Array([1]), new Uint8ClampedArray([1]), new Uint16Array([1]), new Uint32Array([1])]);
// '[{"0":1},{"0":1},{"0":1},{"0":1}]'
JSON.stringify([new Float32Array([1]), new Float64Array([1])]);
// '[{"0":1},{"0":1}]'

// toJSON()
JSON.stringify({ x: 5, y: 6, toJSON(){ return this.x + this.y; } });
// '11'

// Symbols:
JSON.stringify({ x: undefined, y: Object, z: Symbol('') });
// '{}'
JSON.stringify({ [Symbol('foo')]: 'foo' });
// '{}'
JSON.stringify({ [Symbol.for('foo')]: 'foo' }, [Symbol.for('foo')]);
// '{}'
JSON.stringify({ [Symbol.for('foo')]: 'foo' }, function(k, v) {
  if (typeof k === 'symbol') {
    return 'a symbol';
  }
});
// undefined

// Non-enumerable properties:
JSON.stringify( Object.create(null, { x: { value: 'x', enumerable: false }, y: { value: 'y', enumerable: true } }) );
// '{"y":"y"}'

// BigInt values throw
JSON.stringify({x: 2n});
// TypeError: BigInt value can't be serialized in JSON

```

Note: Properties of non-array objects are not guaranteed to be stringified in any particular order. Do not rely on ordering of properties within the same object within the stringification.
```js
var a = JSON.stringify({ foo: "bar", baz: "quux" })
//'{"foo":"bar","baz":"quux"}'
var b = JSON.stringify({ baz: "quux", foo: "bar" })
//'{"baz":"quux","foo":"bar"}'
console.log(a !== b) // true

// some memoization functions use JSON.stringify to serialize arguments,
// which may cause a cache miss when encountering the same object like above

```

##### toJSON() behavior
- If an object being stringified has a property named toJSON whose value is a function, then the toJSON() method customizes JSON stringification behavior: instead of the object being serialized, the value returned by the toJSON() method when called will be serialized. 
\
JSON.stringify() calls toJSON with one parameter:

- if this object is a property value, the property name
- if it is in an array, the index in the array, as a string
- an empty string if JSON.stringify() was directly called on this object

```js
var obj = {
    data: 'data',

    toJSON (key) {
        if (key)
            return `Now I am a nested object under key '${key}'`;
        else
            return this;
    }
};

JSON.stringify(obj);
// '{"data":"data"}'

JSON.stringify({ obj }); // Shorthand property names (ES2015).
// '{"obj":"Now I am a nested object under key 'obj'"}'

JSON.stringify([ obj ]);
// '["Now I am a nested object under key '0'"]'

```

#### References :
- [Working with JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JSON](https://developer.mozilla.org/en-US/docs/Glossary/JSON)
- [Introducing JSON](https://www.json.org/json-en.html)
- [JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
- [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- []()
- []()
- []()
- []()
- []()
- []()
- []()
- []()
- []()
- []()