## Chapter 2 (Draft)

# What You Need To Know About JSON And Objects

&nbsp;&nbsp;&nbsp;&nbsp;Many times, I have received a feedback from my peers that, I can do this crazy thing cause I know how to work with JSON and Objects. And it is surprising. JSON and Objects are one of the most important and very useful concepts in JavaScript. Though, you do not need to know everything about it.

&nbsp;&nbsp;&nbsp;&nbsp;Here, we will learn about some of the most commonly used concepts related to JSON and Objects, That are extermely useful not just when you are working with integrations but elsewhere as well.

## What is JSON

&nbsp;&nbsp;&nbsp;&nbsp;The simplest introduction to JSON I've ever read was in the short presentation on instagram by [codechips](https://www.instagram.com/codechips/?hl=en). I think there is no better way of explaining it than this. I've tweaked the scenerio a bit to make it little familiar, but make sure to look for the original presentation [here](https://www.instagram.com/p/CWTAVdbtKv0/?utm_source=ig_web_copy_link).

&nbsp;&nbsp;&nbsp;&nbsp;Let's say, you are working on the integration between ServiceNow & Google sheet. You want to fetch the information about all the incidents from ServiceNow and store it in google sheet for some reason. But in what format the data should be transferred? The plain text format, as you can notice below, is easy to read but not easy to interpret on client side. Also it is difficult to fetch the individual data from it :

```text
The first incident with number INC0000039 raised by "Bud Richman" have the short description "Trouble getting to Oregon mail server" and the second incident with number INC0000003 raised by "Joe Employee" have the short description "Wireless access is down in my area".
```

&nbsp;&nbsp;&nbsp;&nbsp;Then, the XML was introduced and used very widely, but the format was bulky and much overhead to web service :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
	<result>
		<number>INC0000039</number>
		<short_description>Trouble getting to Oregon mail server</short_description>
		<caller_id>
			<display_value>Bud Richman</display_value>
		</caller_id>
	</result>
	<result>
		<number>INC0000003</number>
		<short_description>Wireless access is down in my area</short_description>
		<caller_id>
			<display_value>Joe Employee</display_value>
		</caller_id>
	</result>
</response>
```

&nbsp;&nbsp;&nbsp;&nbsp;Then, Javascript Object Notation or JSON came into picture. It is faster and easy to read, undersatand & work with:

```json
{
  "result": [
    {
      "number": "INC0000039",
      "short_description": "Trouble getting to Oregon mail server",
      "caller_id": {
        "display_value": "Bud Richman"
      }
    },
    {
      "number": "INC0000003",
      "short_description": "Wireless access is down in my area",
      "caller_id": {
        "display_value": "Joe Employee"
      }
    }
  ]
}
```

&nbsp;&nbsp;&nbsp;&nbsp;So, if you could just use JSON and not XML that would be great.

![XML vs JSON](/images/jlibgkfs8yf21.png)

## Working with JSON

&nbsp;&nbsp;&nbsp;&nbsp;JSON is easy for humans to read and write & for machines to parse and generate. It is supported by many programming languages and is especially useful for JavaScript-based apps, websites and browser extensions.

#### How it looks

- JSON represents numbers, booleans, strings, null, arrays, and objects made up of these values (or of other arrays and objects).
- The curly brackets holds objects.
- The square brackets holds arrays.
- Property names are double-quoted.
- Properties are separated by commas.

&nbsp;&nbsp;&nbsp;&nbsp;Here is an example of a JSON, You are free to play around it :

```json
{
  "first_property_name": "First Property Value of type String",
  "property_name_is_aka_key": 2022,
  "boolean_property_true_or_false": true,
  "null_property": null,
  "array_type_property": ["a", "b", "c"],
  "object_type_property": {
    "number_type_property": 2022
  }
}
```

#### JSON serialization & deserialization

&nbsp;&nbsp;&nbsp;&nbsp;JSON is a syntax for serializing objects, arrays, numbers, strings, booleans, and null. Serialization means to convert an object into that string, and deserialization is its inverse operation.

&nbsp;&nbsp;&nbsp;&nbsp;The JSON object contains methods for parsing JavaScript Object Notation (JSON) and converting values to JSON. We are going to use these methods to see how it works.

#### ServiceNow Scripts - Background

&nbsp;&nbsp;&nbsp;&nbsp;I would like to quote Ben Sweetser as is when it comes to Scripts - Background :

> Scripts - Background was this magical place in the platform where you could run any server-side script. It became my testing ground for any server-side method I wanted to learn about or new script I wanted to test because I did not need to configure When to run logic around it like a Business Rule. Running a script in Scripts - Background was as easy as putting a script in the field and clicking the Run script button.

&nbsp;&nbsp;&nbsp;&nbsp;You can read the article by Ben Sweetser [here](https://developer.servicenow.com/blog.do?p=/post/training-scriptsbg/) if you need to learn more about it.

&nbsp;&nbsp;&nbsp;&nbsp;To open Scripts - Background, use the Application Navigator to open System Definition > Scripts - Background. It is going to be our playground and a friend in our journey.

![Scripts Background](/images/sba.png)

#### typeof & gs.info()

&nbsp;&nbsp;&nbsp;&nbsp;The typeof operator returns a string indicating the type of the value provided, Whereas, gs.info method writes an info message to the system log. Combination of both of them are extremely useful when it comes to debugging but let us use them here for another purpose. You can read more about them typeof [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) and info as well as other useful GlideSystem methods [here](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/server/no-namespace/c_GlideSystemScopedAPI#r_ScopedGlideSystemInf_String_Object_Object_Object_Object_Object).

&nbsp;&nbsp;&nbsp;&nbsp;Copy the following code and paste it into the Scripts - Background.

```js
var jsonObj = {
  Course: "IntegrateNow",
  Skills: ["Integration", "JSON", "ServiceNow"],
  name: {
    first_name: "Vishal",
    last_name: "Ingle",
  },
}

gs.info(jsonObj)
gs.info(typeof jsonObj)
```

![typeof 1](/images/typeof1.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![typeof 2](/images/typeof2.png)

&nbsp;&nbsp;&nbsp;&nbsp;The second line of the output indicates that jsonObj variable stores an object. Though, The first line of the output does not display the content of jsonObj variable.

---

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
const json = '{"result":true, "count":42}'
const obj = JSON.parse(json)

console.log(obj.count)
// expected output: 42

console.log(obj.result)
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
JSON.parse(
  '{"p": 5}',
  (key, value) =>
    typeof value === "number"
      ? value * 2 // return value * 2 for numbers
      : value // return everything else unchanged
)

// { p: 10 }

JSON.parse('{"1": 1, "2": 2, "3": {"4": 4, "5": {"6": 6}}}', (key, value) => {
  console.log(key) // log the current property name, the last is "".
  return value // return the unchanged property value.
})

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
JSON.parse("{}") // {}
JSON.parse("true") // true
JSON.parse('"foo"') // "foo"
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
JSON.parse("null") // null
```

###### Exceptions

- Throws a SyntaxError exception if the string to parse is not valid JSON.
  \
- JSON.parse() does not allow trailing commas

```js
// both will throw a SyntaxError
JSON.parse("[1, 2, 3, 4, ]")
JSON.parse('{"foo" : 1, }')
```

\

- JSON.parse() does not allow single quotes

```js
// will throw a SyntaxError
JSON.parse("{'foo': 1}")
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
console.log(JSON.stringify({ x: 5, y: 6 }))
// expected output: "{"x":5,"y":6}"

console.log(
  JSON.stringify([new Number(3), new String("false"), new Boolean(false)])
)
// expected output: "[3,"false",false]"

console.log(JSON.stringify({ x: [10, undefined, function () {}, Symbol("")] }))
// expected output: "{"x":[10,null,null,null]}"

console.log(JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)))
// expected output: ""2006-01-02T15:04:05.000Z""
```

###### replacer Optional

- A function that alters the behavior of the stringification process, or an array of String and Number that serve as an allowlist for selecting/filtering the properties of the value object to be included in the JSON string.
- If this value is null or not provided, all properties of the object are included in the resulting JSON string.
- The replacer parameter can be either a function or an array.

Example replacer, as a function \

- As a function, it takes two parameters: the key and the value being stringified.
- The object in which the key was found is provided as the replacer's this parameter.
  \
- Initially, the replacer function is called with an empty string as key representing the object being stringified.
- It is then called for each property on the object or array being stringified.
  \
  It should return the value that should be added to the JSON string, as follows:

- If you return a Number, String, Boolean, or null, the stringified version of that value is used as the property's value.
- If you return a Function, Symbol, or undefined, the property is not included in the output.
- If you return any other object, the object is recursively stringified, calling the replacer function on each property.

```js
function replacer(key, value) {
  // Filtering out properties
  if (typeof value === "string") {
    return undefined
  }
  return value
}

var foo = {
  foundation: "Mozilla",
  model: "box",
  week: 45,
  transport: "car",
  month: 7,
}
JSON.stringify(foo, replacer)
// '{"week":45,"month":7}'
```

Example replacer, as an array \
If replacer is an array, the array's values indicate the names of the properties in the object that should be included in the resulting JSON string.

```js
JSON.stringify(foo, ["week", "month"])
// '{"week":45,"month":7}', only keep "week" and "month" properties
```

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
JSON.stringify({ uno: 1, dos: 2 }, null, "\t")
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
JSON.stringify({}) // '{}'
JSON.stringify(true) // 'true'
JSON.stringify("foo") // '"foo"'
JSON.stringify([1, "false", false]) // '[1,"false",false]'
JSON.stringify([NaN, null, Infinity]) // '[null,null,null]'
JSON.stringify({ x: 5 }) // '{"x":5}'

JSON.stringify(new Date(2006, 0, 2, 15, 4, 5))
// '"2006-01-02T15:04:05.000Z"'

JSON.stringify({ x: 5, y: 6 })
// '{"x":5,"y":6}'
JSON.stringify([new Number(3), new String("false"), new Boolean(false)])
// '[3,"false",false]'

// String-keyed array elements are not enumerable and make no sense in JSON
let a = ["foo", "bar"]
a["baz"] = "quux" // a: [ 0: 'foo', 1: 'bar', baz: 'quux' ]
JSON.stringify(a)
// '["foo","bar"]'

JSON.stringify({ x: [10, undefined, function () {}, Symbol("")] })
// '{"x":[10,null,null,null]}'

// Standard data structures
JSON.stringify([
  new Set([1]),
  new Map([[1, 2]]),
  new WeakSet([{ a: 1 }]),
  new WeakMap([[{ a: 1 }, 2]]),
])
// '[{},{},{},{}]'

// TypedArray
JSON.stringify([new Int8Array([1]), new Int16Array([1]), new Int32Array([1])])
// '[{"0":1},{"0":1},{"0":1}]'
JSON.stringify([
  new Uint8Array([1]),
  new Uint8ClampedArray([1]),
  new Uint16Array([1]),
  new Uint32Array([1]),
])
// '[{"0":1},{"0":1},{"0":1},{"0":1}]'
JSON.stringify([new Float32Array([1]), new Float64Array([1])])
// '[{"0":1},{"0":1}]'

// toJSON()
JSON.stringify({
  x: 5,
  y: 6,
  toJSON() {
    return this.x + this.y
  },
})
// '11'

// Symbols:
JSON.stringify({ x: undefined, y: Object, z: Symbol("") })
// '{}'
JSON.stringify({ [Symbol("foo")]: "foo" })
// '{}'
JSON.stringify({ [Symbol.for("foo")]: "foo" }, [Symbol.for("foo")])
// '{}'
JSON.stringify({ [Symbol.for("foo")]: "foo" }, function (k, v) {
  if (typeof k === "symbol") {
    return "a symbol"
  }
})
// undefined

// Non-enumerable properties:
JSON.stringify(
  Object.create(null, {
    x: { value: "x", enumerable: false },
    y: { value: "y", enumerable: true },
  })
)
// '{"y":"y"}'

// BigInt values throw
JSON.stringify({ x: 2n })
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
  data: "data",

  toJSON(key) {
    if (key) return `Now I am a nested object under key '${key}'`
    else return this
  },
}

JSON.stringify(obj)
// '{"data":"data"}'

JSON.stringify({ obj }) // Shorthand property names (ES2015).
// '{"obj":"Now I am a nested object under key 'obj'"}'

JSON.stringify([obj])
// '["Now I am a nested object under key '0'"]'
```

&nbsp;&nbsp;&nbsp;&nbsp;

##

&nbsp;&nbsp;&nbsp;&nbsp;

####

-
-
-
-

![](/images/*.png)

## What's next?

&nbsp;&nbsp;&nbsp;&nbsp; In next chapter, we are actually starting our adventure in the ServiceNow land. I will explain one of the simplest real life use case and start gathering what all is needed to start implementing it. We will talk about ServiceNow API documentation (REST API Explorer), Will understand how to use it, touch back and expand some of the concepts we saw already and introduce some new ones. It will be fun, if you do it by yourself, if not already.
