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

### Static methods
#### JSON.parse(text[, reviver])
- Parse the string text as JSON, optionally transform the produced value and its properties, and return the value. 
- Any violations of the JSON syntax, including those pertaining to the differences between JavaScript and JSON, cause a SyntaxError to be thrown.
- The reviver option allows for interpreting what the replacer has used to stand in for other datatypes.

#### JSON.stringify(value[, replacer[, space]])
- Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner. 
- By default, all instances of undefined are replaced with null, and other unsupported native data types are censored. 
- The replacer option allows for specifying other behavior.

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



#### References :
- [Working with JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JSON](https://developer.mozilla.org/en-US/docs/Glossary/JSON)
- [Introducing JSON](https://www.json.org/json-en.html)
- [JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
- []()