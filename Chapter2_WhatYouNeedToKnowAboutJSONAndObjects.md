## Chapter 2

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

&nbsp;&nbsp;&nbsp;&nbsp;The second line of the output indicates that jsonObj variable stores an object. Though, notice that the first line of the output does not display the content of jsonObj variable.

#### JSON serialization & deserialization

&nbsp;&nbsp;&nbsp;&nbsp;JSON is a syntax for serializing objects, arrays, numbers, strings, booleans, and null. Serialization means to convert an object into that string, and deserialization is its inverse operation.

#### JSON.stringify(value[, replacer[, space]])

&nbsp;&nbsp;&nbsp;&nbsp;The JSON.stringify() method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified. Following are three variations of the method and we will go through each of them one by one :

```js
JSON.stringify(value)
JSON.stringify(value, replacer)
JSON.stringify(value, replacer, space)
```

##### JSON.stringify(value)

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

gs.info(JSON.stringify(jsonObj))
var jsonStr = JSON.stringify(jsonObj)
gs.info(jsonStr)
gs.info(typeof jsonStr)
```

![json 1](/images/json1.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json2.png)

&nbsp;&nbsp;&nbsp;&nbsp;The first and second line of output displays the stringified version of JSON object and the third line indicates that it is of type string.

##### JSON.stringify(value, replacer) & JSON.stringify(value, replacer, space)

&nbsp;&nbsp;&nbsp;&nbsp;Before we talk about the second parameter, replacer, I would like you to be familiar with the third parameter i.e. space. It can be a String or Number object that's used to insert white space (including indentation, line break characters, etc.) into the output JSON string for readability purposes.

- If this parameter is not provided (or is null), no white space is used.
- If this is a Number, it indicates the number of space characters to use as white space for indenting purposes; this number is capped at 10 (if it is greater, the value is just 10).
- Values less than 1 indicate that no space should be used.
- If this is a String, the string (or the first 10 characters of the string, if it's longer than that) is used as white space.
- If it is a number, successive levels in the stringification will each be indented by this many space characters (up to 10).
- If it is a string, successive levels will be indented by this string (or the first ten characters of it).

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

gs.info(JSON.stringify(jsonObj, null, 4))
gs.info(JSON.stringify(jsonObj, null, "\t"))
```

![json 1](/images/json3.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json4.png)

&nbsp;&nbsp;&nbsp;&nbsp;Both the outputs are now displayed in more readable format.

&nbsp;&nbsp;&nbsp;&nbsp;Finally, Let us talk about the second parameter, replacer. It can be a function that alters the behavior of the stringification process, or an array of String and Number that serve as an allowlist for selecting/filtering the properties of the value object to be included in the JSON string. If this value is null or not provided, all properties of the object are included in the resulting JSON string.

&nbsp;&nbsp;&nbsp;&nbsp;The replacer parameter can be either a function or an array.

###### replacer, as an array

If replacer is an array, the array's values indicate the names of the properties in the object that should be included in the resulting JSON string.

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

gs.info(JSON.stringify(jsonObj, ["Course", "Skills"], 4))
gs.info(JSON.stringify(jsonObj, ["Course", "Skills"]))
```

![json 1](/images/json5.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json6.png)

&nbsp;&nbsp;&nbsp;&nbsp;As you might have noticed already, only course and skills are the properties that are added to the new JSON string.

###### replacer, as a function :

- As a function, it takes two parameters: the key and the value being stringified.
- The object in which the key was found is provided as the replacer's this parameter.
- Initially, the replacer function is called with an empty string as key representing the object being stringified.
- It is then called for each property on the object or array being stringified.

It should return the value that should be added to the JSON string, as follows:

- If you return a Number, String, Boolean, or null, the stringified version of that value is used as the property's value.
- If you return a Function, Symbol, or undefined, the property is not included in the output.
- If you return any other object, the object is recursively stringified, calling the replacer function on each property.

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

gs.info(JSON.stringify(jsonObj, replacer))
gs.info(JSON.stringify(jsonObj, replacer, 4))

function replacer(key, value) {
  if (typeof value == "string") {
    return "test_" + value
  }
  return value
}
```

![json 1](/images/json7.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json8.png)

&nbsp;&nbsp;&nbsp;&nbsp;We have modified every string value using our replacer function and appended by "test\_".

&nbsp;&nbsp;&nbsp;&nbsp;We have seen examples of JSON.stringify() and how it works. It converts a value to JSON notation representing it:

- Boolean, Number, and String objects are converted to the corresponding primitive values during stringification.
- undefined, Functions, and Symbols are not valid JSON values. If any such values are encountered during conversion they are either omitted (when found in an object) or changed to null (when found in an array). JSON.stringify() can return undefined when passing in "pure" values like JSON.
- The numbers Infinity and NaN, as well as the value null, are all considered null.
- If the value has a toJSON() method, it's responsible to define what data will be serialized.

#### JSON.parse(text[, reviver])

&nbsp;&nbsp;&nbsp;&nbsp;The JSON.parse() method parses a JSON string, constructing the JavaScript value or object described by the string. It parses the string text as JSON, optionally transform the produced value and its properties, and return the value. Following are three variations of the method and we will go through each of them one by one :

```js
JSON.parse(text)
JSON.parse(text, reviver)
```

&nbsp;&nbsp;&nbsp;&nbsp;Copy the following code and paste it into the Scripts - Background.

```js
var jsonObj = {
  Course: "test_IntegrateNow",
  Skills: ["test_Integration", "test_JSON", "test_ServiceNow"],
  name: {
    first_name: "test_Vishal",
    last_name: "test_Ingle",
  },
}

var jsonStr = JSON.stringify(jsonObj)
gs.info(jsonStr)
gs.info(typeof jsonStr)

gs.info(JSON.parse(jsonStr))
var jsonObjFromString = JSON.parse(jsonStr)
gs.info(jsonObjFromString)
gs.info(typeof jsonObjFromString)
```

![json 1](/images/json9.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json10.png)

&nbsp;&nbsp;&nbsp;&nbsp;After executing the code we are certain that jsonStr is a string and line two of output conveys that. JSON.parse() method converts this json string into an JSON object, last line of the output shows that jsonObjFromString is now an object.

##### Using the reviver parameter

&nbsp;&nbsp;&nbsp;&nbsp;An optional reviver function can be provided to perform a transformation on the resulting object before it is returned or in other words, If a reviver is specified, the value computed by parsing is transformed before being returned. It allows for interpreting what the replacer has used to stand in for other datatypes.

- The computed value and all its properties (beginning with the most nested properties and proceeding to the original value itself) are individually run through the reviver.
- Then it is called, with the object containing the property being processed as this, and with the property name as a string, and the property value as arguments.
- If the reviver function returns undefined (or returns no value, for example, if execution falls off the end of the function), the property is deleted from the object.
- Otherwise, the property is redefined to be the return value.
- If the reviver only transforms some values and not others, be certain to return all untransformed values as-is, otherwise, they will be deleted from the resulting object.

&nbsp;&nbsp;&nbsp;&nbsp;Copy the following code and paste it into the Scripts - Background.

```js
var jsonObj = {
  Course: "test_IntegrateNow",
  Skills: ["test_Integration", "test_JSON", "test_ServiceNow"],
  name: {
    first_name: "test_Vishal",
    last_name: "test_Ingle",
  },
}

var jsonStr = JSON.stringify(jsonObj)

var jsonObjFromString = JSON.parse(jsonStr, reviver)

gs.info(JSON.stringify(jsonObjFromString, null, 4))

function reviver(key, value) {
  if (typeof value === "string") {
    return value.toString().slice(5)
  } else {
    return value
  }
}
```

![json 1](/images/json11.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json12.png)

&nbsp;&nbsp;&nbsp;&nbsp;We have modified every string value using our reviver function and removed "test\_" from it, Output shows the stringified version of this modified object.

&nbsp;&nbsp;&nbsp;&nbsp;We have seen examples of JSON.parse() and how it works. If you are interested in learning more about JSON and its methods, Mozilla developer documentation is a best place to start with, It has everything you need right [here](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON).

&nbsp;&nbsp;&nbsp;&nbsp;Hey, we are not done yet, There are still few more things we need to know.

#### Working with JSON properties

&nbsp;&nbsp;&nbsp;&nbsp;We have kind of already touched these concepts, but let us be more specific to them because they are far more important and needful to us.

&nbsp;&nbsp;&nbsp;&nbsp;we could then access the data inside an object using the dot or bracket notation. An object property can itself be an object, to access these items you just need to chain the extra step onto the end with another dot or bracket. We can also set (update) the value of object members by declaring the member the same way. Let us look at the example to understand what I mean.

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

gs.info(JSON.stringify(jsonObj, null, 4))
gs.info(jsonObj.Course)
gs.info(jsonObj.name.first_name)
gs.info(jsonObj["Course"])
gs.info(jsonObj["name"]["first_name"])

jsonObj.chapter = "Chapter 2"
jsonObj["title"] = "What you need to know abour JSON and Objects"

gs.info(JSON.stringify(jsonObj, null, 4))
```

![json 1](/images/json13.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json14.png)

&nbsp;&nbsp;&nbsp;&nbsp;First we did display the stringified version of initial JSON Object. Next we did log the properties course and first_name from object using dot notation and brackets notation both. Though we have received the same response, it is best to use dot notation for performance reasons. but brackets notation has it's own use cases e.g. if you want to access the array type property's elements. After that we did add two more properties to our object using both dot and brackets notation and then logged the stringified version of object. We can see that our object now contains two new properties chapter & title.

###### Object.keys() & hasOwnProperty()

&nbsp;&nbsp;&nbsp;&nbsp;The Object.keys() method returns an array of a given object's own enumerable property names. And the hasOwnProperty() method returns a boolean indicating whether the object has the specified property as its own property.

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

gs.info(Object.keys(jsonObj))
gs.info(jsonObj.hasOwnProperty("Skills"))
gs.info(jsonObj.hasOwnProperty("more_skills"))
```

![json 1](/images/json15.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now click the Run Script button to execute the script. You should see the following output :
![json 2](/images/json16.png)

&nbsp;&nbsp;&nbsp;&nbsp;The first line of output lists all the property names of our objects. Line two of our output indicates that we have the property named Skills in our object. Line three does indicate the same by returning false.

&nbsp;&nbsp;&nbsp;&nbsp;Finally, We did reach to the end of this chapter. This is the minimum you need to know about JSON and Objects to follow along with me. If you want to dig deep, Mozilla is again the best platform right [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) to learn about objects.

---

## What's next?

&nbsp;&nbsp;&nbsp;&nbsp; In next chapter, we are actually starting our adventure in the ServiceNow land. I will explain one of the simplest real life use case and start gathering what all is needed to start implementing it. We will talk about ServiceNow API documentation (REST API Explorer), Will understand how to use it, touch back and expand some of the concepts we saw already and introduce some new ones. It will be fun, if you do it by yourself, if not already.
