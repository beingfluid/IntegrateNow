## Chapter 6

# Working With XMLs

&nbsp;&nbsp;&nbsp;&nbsp;So far, we have worked with easier JSON responses, but often we need to work with other types e.g. XML, YAML or CSV. Understanding how to work with XMLs is extermely important not only when you work with web services like RSS or SOAP, but also REST when you receive back the responses in XML format. In this chapter, we will try to learn some of the important concepts regarding XML that will help us to work with XML when we interact with them. Here, we will try to limit ourselves to only concepts essential to work with ServiceNow web services and it is extremely important that we understand them very well. If you want to learn more about these concepts, the best place is [XML Tutorial](https://www.w3schools.com/xml/default.asp) on w3schools.com.

![xml](./images/xml-conversion.png)

&nbsp;&nbsp;&nbsp;&nbsp;**XML** or **Extensible Markup Language** is a markup language much like HTML, but without predefined tags to use. Instead, you define your own tags designed specifically for your needs. **XML was designed and is a powerful way to store and transport data in a format that can be both human and machine-readable.** Because of the custom tags, it's something that humans can read and understand. Web services use XML to code and to decode data, and SOAP to transport it.
![XMLResponse](./images/1_XuRqFNT2fMExddcrERq-6g.jpeg)
&nbsp;&nbsp;&nbsp;&nbsp;Many finds working with XML difficult because of its structured nature, which requires more efforts for parsing the XML document. But once you understand the magic that is known as XML, you will be amazed with it's capabilities. And most important thing about XML is, it is everywhere!
![XMLResponse](./images/1m5efq.jpg)

## Structure of an XML document

&nbsp;&nbsp;&nbsp;&nbsp;XML describes a class of data objects called XML documents. The whole structure of XML is built on tags. Use the Application Navigator to open **REST > REST API Explorer**:
![XML1](./images/XML1.png)
&nbsp;&nbsp;&nbsp;&nbsp;In the top-left of the REST API Explorer, Make sure that method selected is **Retrieve records from a table (GET)**. In the Path Parameters section, select the **Incident (incident)** table.
![XML2](./images/XML2.png)
&nbsp;&nbsp;&nbsp;&nbsp;The response by default will return all the incident fields, but we will only need a couple of the fields back in our response, We can specify those in the **sysparm_fields** parameter. Let us limit sysparm_fields to Number, Caller and Short Description:
![XML3](./images/XML3.png)
![XML4](./images/XML4.png)
&nbsp;&nbsp;&nbsp;&nbsp;Let us change the Reesponse format to **application/xml** and click **Send**.
![XML7](./images/XML7.png)

&nbsp;&nbsp;&nbsp;&nbsp;Observe the response body. This, like JSON, is a single line response that we received and is difficult to read:
![XML8](./images/XML8.png)

```xml
<?xml version="1.0" encoding="UTF-8"?><response><result><number>INC0000060</number><short_description>Unable to connect to email</short_description><caller_id><link>https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7</link><value>681ccaf9c0a8016400b98a06818d57c7</value></caller_id></result></response>
```

&nbsp;&nbsp;&nbsp;&nbsp;Let us copy the response and paste it into online prettifier tools like [JSON formatter](https://jsonformatter.org/xml-pretty-print) or [Code Beautify](https://codebeautify.org/xml-pretty-print), which will prettify our XML like below :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
	<result>
		<number>INC0000060</number>
		<short_description>Unable to connect to email</short_description>
		<caller_id>
			<link>https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7</link>
			<value>681ccaf9c0a8016400b98a06818d57c7</value>
		</caller_id>
	</result>
</response>
```

![XML9](./images/XML9.png)
![XML10](./images/XML10.png)

&nbsp;&nbsp;&nbsp;&nbsp;Here, The document starts with a `<response>` tag, followed by a `<result>` element that gives the information about the incident i.e Number, Short Description and Caller. Also, The tags are closed in a sequence; `<response>` tag is closed after the `<result>` tag with the use of `/` character.

&nbsp;&nbsp;&nbsp;&nbsp;However, notice the very first line of our example, which is also known as **XML prolog**:

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

&nbsp;&nbsp;&nbsp;&nbsp;The above line of code is not a tag. It is used just for the transmission of the meta-data of a document i.e. version & character encoding used in the document. The XML prolog is optional. If it exists, it must come first in the document.

&nbsp;&nbsp;&nbsp;&nbsp;**XML documents form a tree structure that starts at "the root" and branches to "the leaves".** The XML above is quite self-descriptive:

- It has a information about Incident Number i.e. `INC0000060` specified in the `number` tag.
- It has a information about incident Short Description i.e. `Unable to connect to email` specified in the `short_description` tag.
- It has a a information about incident Caller specified in the `caller_id` tag. Element `caller_id` has the two child elements:
  - `link` tag provides the API endpoint, which can be used to fetch information about the Incident caller i.e. `https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7`
  - `value` tag provides the SysID of the Incident caller i.e. `681ccaf9c0a8016400b98a06818d57c7`

&nbsp;&nbsp;&nbsp;&nbsp;The tags in the example above (like `<number>` and `<link>`) are not defined in any XML standard. These tags are "invented" by the author of the XML document.

&nbsp;&nbsp;&nbsp;&nbsp;The first line after the prolog defines the **root element** of the document:

```xml
<response>
```

&nbsp;&nbsp;&nbsp;&nbsp;The next line starts a `<result>` element, which is a child element of response:

```xml
<result>
```

&nbsp;&nbsp;&nbsp;&nbsp;The `<result>` element have 3 child elements: `<number>`, `<short_description>` & `<caller_id>`. Similarly, `<caller_id>` have 2 child elements: `<link>` and `<value>`.

&nbsp;&nbsp;&nbsp;&nbsp;One of the important point to remember here is, **XML stores data in plain text format**. This provides a software- and hardware-independent way of storing, transporting, and sharing data.

## The XML Tree Structure

&nbsp;&nbsp;&nbsp;&nbsp;**An XML tree starts at a root element and branches from the root to child elements and all elements can have sub elements (child elements).**

- The terms parent, child, and sibling are used to describe the relationships between elements.
- Parents have children.
- Children have parents.
- Siblings are children on the same level (brothers and sisters).
- All elements can have text content and attributes.

```xml
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```

&nbsp;&nbsp;&nbsp;&nbsp;Consider the below image, copied from [w3schools.com](https://www.w3schools.com/xml/xml_tree.asp):
![nodetree](./images/nodetree.gif)

&nbsp;&nbsp;&nbsp;&nbsp;The image above represents books in this XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
  <book category="cooking">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <price>30.00</price>
  </book>
  <book category="children">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
    <year>2005</year>
    <price>29.99</price>
  </book>
  <book category="web">
    <title lang="en">Learning XML</title>
    <author>Erik T. Ray</author>
    <year>2003</year>
    <price>39.95</price>
  </book>
</bookstore>
```

&nbsp;&nbsp;&nbsp;&nbsp;**An XML element is everything from (including) the element's start tag to (including) the element's end tag** and an element can contain:

- text
- attributes
- other elements
- a mix of the above

&nbsp;&nbsp;&nbsp;&nbsp;In the example above:

- `<title>`, `<author>`, `<year>`, and `<price>` have text content because they contain text (like 29.99).
- `<bookstore>` and `<book>` have element contents, because they contain elements.
- `<book>` has an attribute (`category="children"`).

&nbsp;&nbsp;&nbsp;&nbsp;An element with no content is said to be empty. In XML, you can indicate an empty element like this:

```xml
<business_service></business_service>
```

OR you can also use a so called self-closing tag:

```xml
<business_service/>
```

&nbsp;&nbsp;&nbsp;&nbsp;**XML elements can have attributes, designed to contain data related to a specific element.** Attribute values must always be quoted. Either single or double quotes can be used. E.g. a display_value attribute is used in this example:

```xml
<xml>
    <incident>
        <active>true</active>
        <caller_id  display_value="Joe Employee">681ccaf9c0a8016400b98a06818d57c7</caller_id>
        <category>network</category>
        <short_description>Wireless access is down in my area</short_description>
    </incident>
</xml>
```

&nbsp;&nbsp;&nbsp;&nbsp;**The metadata (data about data) should be stored as attributes, and the data itself should be stored as elements.** E.g. The id attributes below are for identifying the different notes. It is not a part of the note itself.

```xml
<messages>
  <note id="501">
    <to>Tove</to>
    <from>Jani</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend!</body>
  </note>
  <note id="502">
    <to>Jani</to>
    <from>Tove</from>
    <heading>Re: Reminder</heading>
    <body>I will not</body>
  </note>
</messages>
```

## XML design rules

&nbsp;&nbsp;&nbsp;&nbsp;XML document must be well-formed. XML documents that conform to the syntax rules below are said to be "Well Formed" XML documents:

- XML documents must contain one root element that is the parent of all other elements:

```xml
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```

&nbsp;&nbsp;&nbsp;&nbsp;In this example `<response>` is the root element:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
	<result>
		<number>INC0000060</number>
		<short_description>Unable to connect to email</short_description>
		<caller_id>
			<link>https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7</link>
			<value>681ccaf9c0a8016400b98a06818d57c7</value>
		</caller_id>
	</result>
</response>
```

- Element names must start with a letter or underscore.

- Element names cannot start with the letters xml (or XML, or Xml, etc).

- Element names can contain letters, digits, hyphens, underscores, and periods.

- Element names cannot contain spaces.

- In XML, it is illegal to omit the closing tag. All elements must have a closing tag:

```xml
<actions_taken/>
<active>true</active>
```

- XML tags are case sensitive. The tag `<Active>` is different from the tag `<active>`. Opening and closing tags must be written with the same case:

```xml
<short_description>Wireless access is down in my area</short_description>
```

- In XML, all elements must be properly nested within each other. E.g. In the example below, "Properly nested" simply means that since the `<active>` element is opened inside the `<incident>` element, it must be closed inside the `<incident>` element:

```xml
<incident>
  <active>true</active>
</incident>
```

- XML elements can have attributes in name/value pairs just like in HTML. In XML, the attribute values must always be quoted:

```xml
<assignment_group display_value="Incident Management" name="Incident Management">12a586cd0bb23200ecfd818393673a30</assignment_group>
```

- Some characters have a special meaning in XML, they should be replaced with an entity reference. E.g. If you place a character like "<" inside an XML element, it will generate an error because the parser interprets it as the start of a new element and it should be replaced with an entity reference `&lt;`:

```xml
<message>salary &lt; 1000</message>
```

- XML stores a new line as LF.

- Avoid "-". If you name something "first-name", some software may think you want to subtract "name" from "first".

- Avoid ".". If you name something "first.name", some software may think that "name" is a property of the object "first".

- Avoid ":". Colons are reserved for namespaces.

## XML DOM

&nbsp;&nbsp;&nbsp;&nbsp;The **XML DOM defines a standard way for accessing and manipulating XML documents.** It presents an XML document as a tree-structure. The XML DOM is a standard for how to get, change, add, and delete XML elements. All XML elements can be accessed through the XML DOM. Understanding the DOM is a must for anyone working with XML. You can use online tools such [XML Viewer](https://www.xmlviewer.org/) to visualize a tree structure of our XML document:
![XMLTreeView](./images/XMLTreeView.png)

## XML Parser & XMLDocument2

&nbsp;&nbsp;&nbsp;&nbsp;XML parser can convert text into an XML DOM object. ServiceNow provides a JavaScript Object wrapper for parsing and extracting XML data from an XML string known as **XMLDocument2**. An XML string has a tree structure, and the parts of the structure are called nodes. An XMLDocument2 object deals with two node types: element, and document element (root node of the XML tree).

&nbsp;&nbsp;&nbsp;&nbsp;Let us generate the snippet for the GET method that we did use earlier to receive Incident information:

- To create the code sample, Navigate back to REST API Explorer window and click the link for the language of your choice in the REST API Explorer. For the sake of this example, we will select **"ServiceNow Script"**.
  ![XML11](./images/XML11.png)
- To highlight the code sample for copying, click the **Select Snippet** button.
  ![XML12](./images/XML12.png)
- After highlighting the code sample, **copy the code sample to the clipboard** by using ctrl+c.
  ![XML13](./images/XML13.png)

&nbsp;&nbsp;&nbsp;&nbsp;If you did everything correctly you should have the code which look similar to the following copied to your clipboard:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "admin"
var password = "admin"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()
gs.log(response.getBody())
```

&nbsp;&nbsp;&nbsp;&nbsp;It is time to visit our old good friend. Use the Application Navigator to open **System Definition > Scripts - Background** and Paste the snippet that we did copy from last step into the Run Script field.
![XML14](./images/XML14.png)
&nbsp;&nbsp;&nbsp;&nbsp;Let us modify our code to change the fake credentials by your admin credentials, and re-execute the script and Click the **Run script** button to view the results of the script:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()
gs.log(response.getBody())
```

![XML15](./images/XML15.png)
![XML16](./images/XML16.png)

&nbsp;&nbsp;&nbsp;&nbsp;Well, we received the XML response back from our API, but just like JSON responses, it is a XML string. Let us add **typeof** to the logger function to get the type of our response and re-execute the script:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()
gs.log(typeof response.getBody())
```

![XML17](./images/XML17.png)
![XML18](./images/XML18.png)

### XMLDocument2 & parseXML

&nbsp;&nbsp;&nbsp;&nbsp;**XMLDocument2() Creates an XMLDocument2 object.** we can use JavaScript class "XMLDocument2" to create an object from an XML string. **parseXML** method parses the XML string and loads it into the XMLDocument2 object. Lets modify our code and re-execute the script:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

gs.log(typeof xmlDoc)
gs.log(xmlDoc)
```

![XML19](./images/XML19.png)

&nbsp;&nbsp;&nbsp;&nbsp;As we can see from the output, we have converted our string representation of XML into XMLDocument2 object.

![XML20](./images/XML20.png)

### getDocumentElement

&nbsp;&nbsp;&nbsp;&nbsp;**getDocumentElement** gets the document element node of the XMLdocument2 object. The document element node is the root node. Lets modify our code and re-execute the script:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

//returns the root node of the document tree.
var rootNode = xmlDoc.getDocumentElement()
gs.info(rootNode)
```

![XML21](./images/XML21.png)
![XML22](./images/XML22.png)

### XPath

&nbsp;&nbsp;&nbsp;&nbsp;XPath stands for XML Path Language. **XPath can be used to navigate through elements and attributes in an XML document.** It uses path expressions to navigate in XML documents. These path expressions look very much like the expressions you see when you work with a traditional computer file system.

![img_xpath_folders](./images/xpathwin.png)

&nbsp;&nbsp;&nbsp;&nbsp;XML documents are treated as trees of nodes. In XPath, there are seven kinds of nodes: element, attribute, text, namespace, processing-instruction, comment, and document nodes. The topmost element of the tree is called the root element. Look at the following XML document:

```xml
<?xml version="1.0" encoding="UTF-8"?>

<bookstore>

<book category="cooking">
  <title lang="en">Everyday Italian</title>
  <author>Giada De Laurentiis</author>
  <year>2005</year>
  <price>30.00</price>
</book>

<book category="children">
  <title lang="en">Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>

<book category="web">
  <title lang="en">XQuery Kick Start</title>
  <author>James McGovern</author>
  <author>Per Bothner</author>
  <author>Kurt Cagle</author>
  <author>James Linn</author>
  <author>Vaidyanathan Nagarajan</author>
  <year>2003</year>
  <price>49.99</price>
</book>

<book category="web">
  <title lang="en">Learning XML</title>
  <author>Erik T. Ray</author>
  <year>2003</year>
  <price>39.95</price>
</book>

</bookstore>
```

&nbsp;&nbsp;&nbsp;&nbsp;Example of nodes in the XML document above:

```xml
<bookstore> (root element node)

<author>J K. Rowling</author> (element node)

lang="en" (attribute node)
```

### Selecting Nodes

&nbsp;&nbsp;&nbsp;&nbsp;XPath uses path expressions to select nodes in an XML document. The node is selected by following a path or steps. The most useful path expressions are listed below:

| Expression | Description                                                                                           | Example         | Result                                                                                                                       |
| ---------- | ----------------------------------------------------------------------------------------------------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| nodename   | Selects all nodes with the name "nodename"                                                            | bookstore       | Selects all nodes with the name "bookstore"                                                                                  |
| /          | Selects from the root node                                                                            | /bookstore      | Selects the root element bookstore                                                                                           |
|            |                                                                                                       | bookstore/book  | Selects all book elements that are children of bookstore                                                                     |
| //         | Selects nodes in the document from the current node that match the selection no matter where they are | //book          | Selects all book elements no matter where they are in the document                                                           |
|            |                                                                                                       | bookstore//book | Selects all book elements that are descendant of the bookstore element, no matter where they are under the bookstore element |
| .          | Selects the current node                                                                              |
| ..         | Selects the parent of the current node                                                                |
| @          | Selects attributes                                                                                    | //@             | lang Selects all attributes that are named lang                                                                              |

### Predicates

&nbsp;&nbsp;&nbsp;&nbsp;Predicates are used to find a specific node or a node that contains a specific value. Predicates are always embedded in square brackets. In the table below we have listed some path expressions with predicates and the result of the expressions:

| Path Expression                    | Result                                                                                                                                 |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| /bookstore/book[1]                 | Selects the first book element that is the child of the bookstore element.                                                             |
| /bookstore/book[last()]            | Selects the last book element that is the child of the bookstore element                                                               |
| /bookstore/book[last()-1]          | Selects the last but one book element that is the child of the bookstore element                                                       |
| /bookstore/book[position()<3]      | Selects the first two book elements that are children of the bookstore element                                                         |
| //title[@lang]                     | Selects all the title elements that have an attribute named lang                                                                       |
| //title[@lang='en']                | Selects all the title elements that have a "lang" attribute with a value of "en"                                                       |
| /bookstore/book[price>35.00]       | Selects all the book elements of the bookstore element that have a price element with a value greater than 35.00                       |
| /bookstore/book[price>35.00]/title | Selects all the title elements of the book elements of the bookstore element that have a price element with a value greater than 35.00 |

### Selecting Unknown Nodes

&nbsp;&nbsp;&nbsp;&nbsp;XPath wildcards can be used to select unknown XML nodes. In the table below we have listed some path expressions and the result of the expressions:

| Wildcard | Description                  | Path Expression | Result                                                                   |
| -------- | ---------------------------- | --------------- | ------------------------------------------------------------------------ |
| \*       | Matches any element node     | /bookstore/\*   | Selects all the child element nodes of the bookstore element             |
|          |                              | //\*            | Selects all elements in the document                                     |
| @\*      | Matches any attribute node   | //title[@*]     | Selects all title elements which have at least one attribute of any kind |
| node()   | Matches any node of any kind |                 |                                                                          |

### Selecting Several Paths

&nbsp;&nbsp;&nbsp;&nbsp;By using the **|** operator in an XPath expression you can select several paths. In the table below we have listed some path expressions and the result of the expressions:

| Path Expression                  | Result                                                                                                                 |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| //book/title \| //book/price     | Selects all the title AND price elements of all book elements                                                          |
| //title \| //price               | Selects all the title AND price elements in the document                                                               |
| /bookstore/book/title \| //price | Selects all the title elements of the book element of the bookstore element AND all the price elements in the document |

### XPath Axes

&nbsp;&nbsp;&nbsp;&nbsp;An axis represents a relationship to the context (current) node, and is used to locate nodes relative to that node on the tree.

| AxisName           | Result                                                                                                                       |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| ancestor           | Selects all ancestors (parent, grandparent, etc.) of the current node                                                        |
| ancestor-or-self   | Selects all ancestors (parent, grandparent, etc.) of the current node and the current node itself                            |
| attribute          | Selects all attributes of the current node                                                                                   |
| child              | Selects all children of the current node                                                                                     |
| descendant         | Selects all descendants (children, grandchildren, etc.) of the current node                                                  |
| descendant-or-self | Selects all descendants (children, grandchildren, etc.) of the current node and the current node itself                      |
| following          | Selects everything in the document after the closing tag of the current node                                                 |
| following-sibling  | Selects all siblings after the current node                                                                                  |
| namespace          | Selects all namespace nodes of the current node                                                                              |
| parent             | Selects the parent of the current node                                                                                       |
| preceding          | Selects all nodes that appear before the current node in the document, except ancestors, attribute nodes and namespace nodes |
| preceding-sibling  | Selects all siblings before the current node                                                                                 |
| self               | Selects the current node                                                                                                     |

### Location Path Expression

&nbsp;&nbsp;&nbsp;&nbsp;A location path can be absolute or relative. An absolute location path starts with a slash ( / ) and a relative location path does not. In both cases the location path consists of one or more steps, each separated by a slash:

```xml
An absolute location path:

/step/step/...

A relative location path:

step/step/...
```

&nbsp;&nbsp;&nbsp;&nbsp;The syntax for a location step is:

```xml
axisname::nodetest[predicate]
```

| Example                | Result                                                                                        |
| ---------------------- | --------------------------------------------------------------------------------------------- |
| child::book            | Selects all book nodes that are children of the current node                                  |
| attribute::lang        | Selects the lang attribute of the current node                                                |
| child::\*              | Selects all element children of the current node                                              |
| attribute::\*          | Selects all attributes of the current node                                                    |
| child::text()          | Selects all text node children of the current node                                            |
| child::node()          | Selects all children of the current node                                                      |
| descendant::book       | Selects all book descendants of the current node                                              |
| ancestor::book         | Selects all book ancestors of the current node                                                |
| ancestor-or-self::book | Selects all book ancestors of the current node - and the current as well if it is a book node |
| child::\*/child::price | Selects all price grandchildren of the current node                                           |

### getNode & getNodeText

&nbsp;&nbsp;&nbsp;&nbsp;**getNode** gets the node specified in the xPath. **getNodeText** gets all the text child nodes from the node referenced in the specified XPath. Let us modify our code to fetch the `number` element from our response and re-execute the script:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

var node = xmlDoc.getNode("/response/result/number")
gs.info(node)
```

![XML26](./images/XML26.png)
&nbsp;&nbsp;&nbsp;&nbsp;Your output should look something like this:

```xml
<number>INC0000060</number>
```

&nbsp;&nbsp;&nbsp;&nbsp;If you are wondering how the result of the background script is displayed on the same page, that is probabaly because you are unaware of an awesome extension [SN Utils](https://www.arnoudkooi.com/) by Arnoud Kooi. I strongly encourage you to have this extension installed on your personal computer to learn the amazing capabilities of this extension and increase your productivity.

&nbsp;&nbsp;&nbsp;&nbsp;Now, lets modify the script one more time to get the incident number from number element:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

var nodeText = xmlDoc.getNodeText("/response/result/number")
gs.info(nodeText)
```

&nbsp;&nbsp;&nbsp;&nbsp;After executing the script, your output should look something similar to the following:

```js
INC0000060
```

![XML27](./images/XML27.png)

### getFirstNode & getNextNode

&nbsp;&nbsp;&nbsp;&nbsp;**getFirstNode** gets the first node in the specified xPath. **getNextNode** gets the node after the specified node. Let us assume the following document from [ServiceNow API documentation](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/server/no-namespace/c_XMLDocument2ScopedAPI):

```xml
<store>
    <resources company="ABC Inc">
        <resources type="servers" />
    </resources>
    <resources company="XYZ Inc">
        <resource type="bookstore">
            <book>
                <title>Windows</title>
                <price>10</price>
            </book>
            <book year="2009">
                <title>Harry Potter</title>
                <price>50</price>
            </book>
            <book year="1999">
                <title>Learning XML</title>
                <price>120</price>
            </book>
            <book year="2019">
                <title>Learning Java</title>
                <price>99</price>
            </book>
        </resource>
    </resources>
</store>
```

&nbsp;&nbsp;&nbsp;&nbsp;The getFirstNode methods supports the following xPath expressions with predicates:

`/store/resources/resource[@type='bookstore']/book[@year='1999']`
`/store/resources/resource[@type='bookstore']/book[@year]`
`/store/resources/resource[@type='bookstore']/book[price > 100]`

&nbsp;&nbsp;&nbsp;&nbsp;However, it does not support the following xPath expressions with predicates:

`/store/resources/resource[@type='bookstore']/book[2]`
`/store/resources/resource[@type='bookstore']/book[last()]`
`/store/resources/resource[@type='bookstore']/book[position()>2]`

&nbsp;&nbsp;&nbsp;&nbsp;To work around this, use xPath without predicates, such as `/store/resources/resource[@type='bookstore']/book` and then filter the nodes in the script using the getFirstNode() and getNextNode() methods.

&nbsp;&nbsp;&nbsp;&nbsp;Let us modify our code to fetch information about 3 incidents, by setting the **sysparm_limit** query parameter to 3 :

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=3"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

//returns the root node of the document tree.
var rootNode = xmlDoc.getDocumentElement()
gs.info(rootNode)
```

&nbsp;&nbsp;&nbsp;&nbsp;The above script will log the document element tree structure, which should look something like this :

```xml
<response>
	<result>
		<number>INC0000060</number>
		<short_description>Unable to connect to email</short_description>
		<caller_id>
			<link>https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7</link>
			<value>681ccaf9c0a8016400b98a06818d57c7</value>
		</caller_id>
	</result>
	<result>
		<number>INC0009002</number>
		<short_description>My computer is not detecting the headphone device</short_description>
		<caller_id>
			<link>https://dev124645.service-now.com/api/now/table/sys_user/77ad8176731313005754660c4cf6a7de</link>
			<value>77ad8176731313005754660c4cf6a7de</value>
		</caller_id>
	</result>
	<result>
		<number>INC0000009</number>
		<short_description>Reset my password</short_description>
		<caller_id>
			<link>https://dev124645.service-now.com/api/now/table/sys_user/5137153cc611227c000bbd1bd8cd2006</link>
			<value>5137153cc611227c000bbd1bd8cd2006</value>
		</caller_id>
	</result>
</response>
```

![XML23](./images/XML23.png)

&nbsp;&nbsp;&nbsp;&nbsp;Now, let us observe our output. we have several `result` nodes in our `response` element. To see getFirstNode in action, modify the script as below and re-execute:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=3"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

var firstIncResult = xmlDoc.getFirstNode("/response/result")
gs.info(firstIncResult)
```

![XML24](./images/XML24.png)

&nbsp;&nbsp;&nbsp;&nbsp;You should receive the output displaying the information about first result node, which looks something like this:

```xml
<result>
	<number>INC0000060</number>
	<short_description>Unable to connect to email</short_description>
	<caller_id>
		<link>https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7</link>
		<value>681ccaf9c0a8016400b98a06818d57c7</value>
	</caller_id>
</result>
```

&nbsp;&nbsp;&nbsp;&nbsp;Now, let us modify the script again to see getNextNode in action as below and re-execute:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=3"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

var firstIncResult = xmlDoc.getFirstNode("/response/result")

var secondIncResult = xmlDoc.getNextNode(firstIncResult)
gs.info(secondIncResult)
```

![XML25](./images/XML25.png)

&nbsp;&nbsp;&nbsp;&nbsp;You should receive the output displaying the information about second result node, which looks something like this:

```xml
<result>
	<number>INC0009002</number>
	<short_description>My computer is not detecting the headphone device</short_description>
	<caller_id>
		<link>https://dev124645.service-now.com/api/now/table/sys_user/77ad8176731313005754660c4cf6a7de</link>
		<value>77ad8176731313005754660c4cf6a7de</value>
	</caller_id>
</result>
```

&nbsp;&nbsp;&nbsp;&nbsp;The most important thing to notice here is that the parameter (The current node) passed to the getNextNode method. In our example we passed the first result node **firstIncResult** as a parameter to the getNextNode method in order to retrieve the next result node.

### createElement & createElementWithTextValue

&nbsp;&nbsp;&nbsp;&nbsp;**createElement** creates and adds an element node to the current node. The element name is the string passed in as a parameter. The new element has no text child nodes. **createElementWithTextValue** creates and adds an element node with a text child node to the current node. It accepts two string parameters: name of the element to add & element's text value. Lets modify our script to see these two methods in action:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

xmlDoc.createElement("new_element_without_text")
xmlDoc.createElementWithTextValue(
  "new_element_with_text",
  "New Element With Text"
)

gs.info(xmlDoc)
```

&nbsp;&nbsp;&nbsp;&nbsp;After execution your output should be similar to the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
	<new_element_without_text/>
	<new_element_with_text>New Element With Text</new_element_with_text>
	<result>
		<number>INC0000060</number>
		<short_description>Unable to connect to email</short_description>
		<caller_id>
			<link>https://dev124645.service-now.com/api/now/table/sys_user/681ccaf9c0a8016400b98a06818d57c7</link>
			<value>681ccaf9c0a8016400b98a06818d57c7</value>
		</caller_id>
	</result>
</response>
```

![XML28](./images/XML28.png)

&nbsp;&nbsp;&nbsp;&nbsp;As you can clearly notice, We have two additional nodes added to our document : `new_element_without_text` and `new_element_with_text`.

### xmlToJSON

![xmltojson](./images/xmltojson.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;Though parsing the xml with help of XMLDocument2 is very convinient, We can leverage xmlToJSON method of GlideSystem to convert the xml to JSON object which is easier to work with. **xmlToJSON Takes an XML string and returns a JSON object.** Let us modify the script to understand how this works :

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlObj = gs.xmlToJSON(xmlString)

gs.info(JSON.stringify(xmlObj, null, 4))
```

&nbsp;&nbsp;&nbsp;&nbsp;After executing the script, our **xmlObj** contains the JSON object, the last logger function in our script pretty prints the JSON object:

![XML29](./images/XML29.png)

&nbsp;&nbsp;&nbsp;&nbsp;Though, the script worked totally fine, It is important that you pre-process the XML input before passing to xmlToJSON. You can read more about this in the Support article [KB0784264](https://support.servicenow.com/kb?id=kb_article_view&sysparm_article=KB0784264). The modified script looks similar to this:

```js
var request = new sn_ws.RESTMessageV2()
request.setEndpoint(
  "https://dev124645.service-now.com/api/now/table/incident?sysparm_fields=number%2Ccaller_id%2Cshort_description&sysparm_limit=1"
)
request.setHttpMethod("GET")

//Eg. UserName="admin", Password="admin" for this code sample.
var user = "MyAdminUserName"
var password = "MyAdminPassword"

request.setBasicAuth(user, password)
request.setRequestHeader("Accept", "application/xml")

var response = request.execute()

var xmlString = response.getBody()

var xmlDoc = new XMLDocument2()
xmlDoc.parseXML(xmlString)

var rootNode = xmlDoc.getDocumentElement()

var xmlObj = gs.xmlToJSON(rootNode)

gs.info(JSON.stringify(xmlObj, null, 4))
```

![XML30](./images/XML30.png)

### XMLNode

&nbsp;&nbsp;&nbsp;&nbsp;The scoped XMLNode API allows you to query values from XML nodes. XMLNodes are extracted from XMLDocument2 objects, which contain XML strings.

### XML Namespaces

&nbsp;&nbsp;&nbsp;&nbsp;**XML Namespaces provide a method to avoid element name conflicts.** In XML, element names are defined by the developer. This often results in a conflict when trying to mix XML documents from different XML applications.

&nbsp;&nbsp;&nbsp;&nbsp;This XML carries HTML table information:

```xml
<table>
  <tr>
    <td>Apples</td>
    <td>Bananas</td>
  </tr>
</table>
```

&nbsp;&nbsp;&nbsp;&nbsp;This XML carries information about a table (a piece of furniture):

```xml
<table>
  <name>African Coffee Table</name>
  <width>80</width>
  <length>120</length>
</table>
```

&nbsp;&nbsp;&nbsp;&nbsp; If these XML fragments were added together, there would be a name conflict. Both contain a <table> element, but the elements have different content and meaning. A user or an XML application will not know how to handle these differences:

```xml
<root>

    <table>
    <tr>
        <td>Apples</td>
        <td>Bananas</td>
    </tr>
    </table>

    <table>
    <name>African Coffee Table</name>
    <width>80</width>
    <length>120</length>
    </table>

</root>
```

&nbsp;&nbsp;&nbsp;&nbsp;Name conflicts in XML can easily be avoided using a name prefix. When using prefixes in XML, a namespace for the prefix must be defined using an xmlns attribute in the start tag of an element. The namespace declaration has the following syntax:

```xml
xmlns:prefix="URI"
```

&nbsp;&nbsp;&nbsp;&nbsp;In the example below, there will be no conflict because the two `<table>` elements have different names:

```xml
<root>

<h:table xmlns:h="http://www.w3.org/TR/html4/">
  <h:tr>
    <h:td>Apples</h:td>
    <h:td>Bananas</h:td>
  </h:tr>
</h:table>

<f:table xmlns:f="https://www.w3schools.com/furniture">
  <f:name>African Coffee Table</f:name>
  <f:width>80</f:width>
  <f:length>120</f:length>
</f:table>

</root>
```

&nbsp;&nbsp;&nbsp;&nbsp;Here,

- The xmlns attribute in the first `<table>` element gives the h: prefix a qualified namespace.
- The xmlns attribute in the second `<table>` element gives the f: prefix a qualified namespace.
- When a namespace is defined for an element, all child elements with the same prefix are associated with the same namespace.

&nbsp;&nbsp;&nbsp;&nbsp;Namespaces can also be declared in the XML root element:

```xml
<root xmlns:h="http://www.w3.org/TR/html4/"
xmlns:f="https://www.w3schools.com/furniture">

<h:table>
  <h:tr>
    <h:td>Apples</h:td>
    <h:td>Bananas</h:td>
  </h:tr>
</h:table>

<f:table>
  <f:name>African Coffee Table</f:name>
  <f:width>80</f:width>
  <f:length>120</f:length>
</f:table>

</root>
```

&nbsp;&nbsp;&nbsp;&nbsp;The namespace URI is not used by the parser to look up information. The purpose of using an URI is to give the namespace a unique name. However, It is often used as a pointer to a web page containing namespace information. XMLs are everywhere in ServiceNow platform, but the best place to find the use of namespaces on the ServiceNow platform is UI pages module:
![xmlns](./images/xmlns.png)

## XML Schema

&nbsp;&nbsp;&nbsp;&nbsp;**A document type definition defines the rules and the legal elements and attributes for an XML document.** A "valid" XML document must be well formed. In addition, it must conform to a document type definition.

&nbsp;&nbsp;&nbsp;&nbsp;There are two different document type definitions that can be used with XML:

- **DTD** - The original Document Type Definition
- **XML Schema** - An XML-based alternative to DTD

&nbsp;&nbsp;&nbsp;&nbsp;**An XML document validated against a DTD is both "Well Formed" and "Valid".**

### XML DTD

&nbsp;&nbsp;&nbsp;&nbsp;**A DTD or Document Type Definition defines the structure and the legal elements and attributes of an XML document.** With a DTD, you can verify that the data you receive from the outside world is valid. A "Valid" XML document is "Well Formed", as well as it conforms to the rules of a DTD. Look at this simple XML document called "note.xml", This XML document has a reference to a DTD:

```xml
<?xml version="1.0"?>

<!DOCTYPE note SYSTEM
"https://www.w3schools.com/xml/note.dtd">

<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```

&nbsp;&nbsp;&nbsp;&nbsp;The following example is a DTD file called "note.dtd" that defines the elements of the XML document above ("note.xml"):

```xml
<!DOCTYPE note
[
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
]>
```

&nbsp;&nbsp;&nbsp;&nbsp;The purpose of a DTD is to define the structure and the legal elements and attributes of an XML document. The DTD above is interpreted like this:

- **!DOCTYPE note** - Defines that the root element of the document is note
- **!ELEMENT note** - Defines that the note element must contain the elements: "to, from, heading, body"
- **!ELEMENT to** - Defines the to element to be of type "#PCDATA"
- **!ELEMENT from** - Defines the from element to be of type "#PCDATA"
- **!ELEMENT heading** - Defines the heading element to be of type "#PCDATA"
- **!ELEMENT body** - Defines the body element to be of type "#PCDATA"

### XML Schema

&nbsp;&nbsp;&nbsp;&nbsp;XML Schema is an XML-based alternative to DTD. **An XML Schema describes the structure of an XML document, just like a DTD.** With XML Schema, your XML files can carry a description of its own format. An XML document validated against an XML Schema is both "Well Formed" and "Valid". Let us modify our XML document to have a reference to an XML Schema:

```xml
<?xml version="1.0"?>

<note
xmlns="https://www.w3schools.com"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="https://www.w3schools.com/xml note.xsd">
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```

&nbsp;&nbsp;&nbsp;&nbsp;The line above: `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"` tells the XML parser that this document should be validated against a schema. The line: `xsi:schemaLocation="https://www.w3schools.com/xml note.xsd"` specifies WHERE the schema resides. The following example is an XML Schema file called "note.xsd" that defines the elements of the XML document above ("note.xml"):

```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="https://www.w3schools.com"
xmlns="https://www.w3schools.com"
elementFormDefault="qualified">

<xs:element name="note">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="to" type="xs:string"/>
      <xs:element name="from" type="xs:string"/>
      <xs:element name="heading" type="xs:string"/>
      <xs:element name="body" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

</xs:schema>
```

&nbsp;&nbsp;&nbsp;&nbsp;The Schema above is interpreted like this:

- `<xs:element name="note">` defines the element called "note"
- `<xs:complexType>` the "note" element is a complex type
- `<xs:sequence>` the complex type is a sequence of elements
- `<xs:element name="to" type="xs:string">` the element "to" is of type string (text)
- `<xs:element name="from" type="xs:string">` the element "from" is of type string
- `<xs:element name="heading" type="xs:string">` the element "heading" is of type string
- `<xs:element name="body" type="xs:string">` the element "body" is of type string

&nbsp;&nbsp;&nbsp;&nbsp;The note element is a complex type because it contains other elements. The other elements (to, from, heading, body) are simple types because they do not contain other elements. The XML Schema language is also referred to as XML Schema Definition (XSD). The purpose of an XML Schema is to define the legal building blocks of an XML document:

- the elements and attributes that can appear in a document
- the number of (and order of) child elements
- data types for elements and attributes
- default and fixed values for elements and attributes

&nbsp;&nbsp;&nbsp;&nbsp;One of the greatest strength of XML Schemas is the support for data types:

- It is easier to describe allowable document content
- It is easier to validate the correctness of data
- It is easier to define data facets (restrictions on data)
- It is easier to define data patterns (data formats)
- It is easier to convert data between different data types

&nbsp;&nbsp;&nbsp;&nbsp;When sending data from a sender to a receiver, it is essential that both parts have the same "expectations" about the content. With XML Schemas, the sender can describe the data in a way that the receiver will understand. A date like: "03-11-2004" will, in some countries, be interpreted as 3 November and in other countries as 11 March. However, an XML element with a data type like this:
`<date type="date">2004-03-11</date>`
ensures a mutual understanding of the content, because the XML data type "date" requires the format "YYYY-MM-DD".

### The `<schema>` Element

&nbsp;&nbsp;&nbsp;&nbsp;The <schema> element is the root element of every XML Schema, The <schema> element may contain some attributes:

```xsd
<?xml version="1.0"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="https://www.w3schools.com"
xmlns="https://www.w3schools.com"
elementFormDefault="qualified">
...
...
</xs:schema>
```

- `xmlns:xs="http://www.w3.org/2001/XMLSchema"` indicates that the elements and data types used in the schema come from the `http://www.w3.org/2001/XMLSchema` namespace. It also specifies that the elements and data types that come from the `http://www.w3.org/2001/XMLSchema` namespace should be prefixed with `xs:`.
- `targetNamespace="https://www.w3schools.com"`
  indicates that the elements defined by this schema (note, to, from, heading, body.) come from the `https://www.w3schools.com` namespace.
- `xmlns="https://www.w3schools.com"`
  indicates that the default namespace is `https://www.w3schools.com`.
- `elementFormDefault="qualified"`
  indicates that any elements used by the XML instance document which were declared in this schema must be namespace qualified.

### Referencing a Schema in an XML Document

&nbsp;&nbsp;&nbsp;&nbsp;This XML document has a reference to an XML Schema:

```xml
<?xml version="1.0"?>

<note xmlns="https://www.w3schools.com"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="https://www.w3schools.com note.xsd">

<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```

- `xmlns="https://www.w3schools.com"`
  specifies the default namespace declaration. This declaration tells the schema-validator that all the elements used in this XML document are declared in the `https://www.w3schools.com` namespace.

- Once you have the XML Schema Instance namespace available: `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`, you can use the `schemaLocation` attribute. This attribute has two values, separated by a space. The first value is the namespace to use. The second value is the location of the XML schema to use for that namespace: `xsi:schemaLocation="https://www.w3schools.com note.xsd"`

### XSD Data Types

&nbsp;&nbsp;&nbsp;&nbsp;XML Schema has a lot of built-in data types. The most common types are:

- xs:string
- xs:decimal
- xs:integer
- xs:boolean
- xs:date
- xs:time

#### XSD String Data Types

&nbsp;&nbsp;&nbsp;&nbsp;String data types are used for values that contains character strings. The string data type can contain characters, line feeds, carriage returns, and tab characters. The following is an example of a string declaration in a schema:

```xsd
<xs:element name="customer" type="xs:string"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xml
<customer>John Smith</customer>
```

##### NormalizedString & Token Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The normalizedString & token data type are derived from the String data type. Both also contains characters, but the XML processor will remove line feeds, carriage returns, and tab characters. The following is an example of a normalizedString declaration in a schema:

```xsd
<xs:element name="customer" type="xs:normalizedString"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;The following is an example of a token declaration in a schema:

```xsd
<xs:element name="customer" type="xs:token"/>
```

#### XSD Date and Time Data Types

&nbsp;&nbsp;&nbsp;&nbsp;Date and time data types are used for values that contain date and time.

##### Date Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The date data type is used to specify a date. The date is specified in the following form "YYYY-MM-DD" where:

- **YYYY** indicates the year
- **MM** indicates the month
- **DD** indicates the day

&nbsp;&nbsp;&nbsp;&nbsp;The following is an example of a date declaration in a schema:

```xsd
<xs:element name="start" type="xs:date"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xsd
<start>2002-09-24</start>
```

##### Time Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The time data type is used to specify a time. The time is specified in the following form "hh:mm:ss" where:

- **hh** indicates the hour
- **mm** indicates the minute
- **ss** indicates the second

&nbsp;&nbsp;&nbsp;&nbsp;The following is an example of a time declaration in a schema:

```xsd
<xs:element name="start" type="xs:time"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xsd
<start>09:00:00</start>
```

##### DateTime Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The dateTime data type is used to specify a date and a time. The dateTime is specified in the following form "YYYY-MM-DDThh:mm:ss" where:

- **T** indicates the start of the required time section

&nbsp;&nbsp;&nbsp;&nbsp;The following is an example of a dateTime declaration in a schema:

```xsd
<xs:element name="startdate" type="xs:dateTime"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xsd
<startdate>2002-05-30T09:00:00</startdate>
```

##### Time Zones

&nbsp;&nbsp;&nbsp;&nbsp;To specify a time zone, you can either enter a date, time or dateTime in UTC time by adding a "Z" at the end, like this:

```xml
<startdate>2002-05-30T09:30:10Z</startdate>
```

&nbsp;&nbsp;&nbsp;&nbsp;or you can specify an offset from the UTC time by adding a positive or negative time behind the time - like this:

```xml
<startdate>2002-05-30T09:30:10+06:00</startdate>
```

##### Duration Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The duration data type is used to specify a time interval. The time interval is specified in the following form "PnYnMnDTnHnMnS" where:

- **P** indicates the period (required)
- **nY** indicates the number of years
- **nM** indicates the number of months
- **nD** indicates the number of days
- **nH** indicates the number of hours
- **nM** indicates the number of minutes
- **nS** indicates the number of seconds

&nbsp;&nbsp;&nbsp;&nbsp;The following is an example of a duration declaration in a schema:

```xsd
<xs:element name="period" type="xs:duration"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xsd
<period>P5Y2M10DT15H</period>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example above indicates a period of five years, two months, 10 days, and 15 hours.

#### XSD Numeric Data Types

&nbsp;&nbsp;&nbsp;&nbsp;Decimal data types are used for numeric values.

##### Decimal Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The decimal data type is used to specify a numeric value. The following is an example of a decimal declaration in a schema:

```xsd
<xs:element name="price" type="xs:decimal"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xml
<price>999.50</price>
```

##### Integer Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The integer data type is used to specify a numeric value without a fractional component. The following is an example of an integer declaration in a schema:

```xsd
<xs:element name="price" type="xs:integer"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xml
<price>999</price>
```

#### Boolean Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The boolean data type is used to specify a true or false value. Legal values for boolean are true, false, 1 (which indicates true), and 0 (which indicates false). The following is an example of a boolean declaration in a schema:

```xsd
<xs:attribute name="disabled" type="xs:boolean"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xml
<price disabled="true">999</price>
```

#### AnyURI Data Type

&nbsp;&nbsp;&nbsp;&nbsp;The anyURI data type is used to specify a URI. The following is an example of an anyURI declaration in a schema:

```xsd
<xs:attribute name="src" type="xs:anyURI"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;An element in your document might look like this:

```xml
<pic src="https://www.w3schools.com/images/smiley.gif" />
```

### XSD Simple Elements

&nbsp;&nbsp;&nbsp;&nbsp;XML Schemas define the elements of your XML files. **A simple element is an XML element that contains only text. It cannot contain any other elements or attributes.** However, the text can be of many different types. It can be one of the types included in the XML Schema definition (boolean, string, date, etc.), or it can be a custom type that you can define yourself. You can also add restrictions (facets) to a data type in order to limit its content, or you can require the data to match a specific pattern.

&nbsp;&nbsp;&nbsp;&nbsp;The syntax for defining a simple element is:

```xml
<xs:element name="xxx" type="yyy"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;where xxx is the name of the element and yyy is the data type of the element.

&nbsp;&nbsp;&nbsp;&nbsp;Here is an example of some XML elements:

```xml
<lastname>Refsnes</lastname>
<age>36</age>
<dateborn>1970-03-27</dateborn>
```

&nbsp;&nbsp;&nbsp;&nbsp;The corresponding simple element definitions are:

```xsd
<xs:element name="lastname" type="xs:string"/>
<xs:element name="age" type="xs:integer"/>
<xs:element name="dateborn" type="xs:date"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;Simple elements may have a default value OR a fixed value specified. A default value is automatically assigned to the element when no other value is specified; A fixed value is also automatically assigned to the element, and you cannot specify another value.

- In the following example the default value is "red":

```xml
<xs:element name="color" type="xs:string" default="red"/>
```

- In the following example the fixed value is "red":

```xml
<xs:element name="color" type="xs:string" fixed="red"/>
```

### XSD Attributes

&nbsp;&nbsp;&nbsp;&nbsp;Simple elements cannot have attributes. If an element has attributes, it is considered to be of a complex type. But the attribute itself is always declared as a simple type.

&nbsp;&nbsp;&nbsp;&nbsp;The syntax for defining an attribute is:

```xml
<xs:attribute name="xxx" type="yyy"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;where xxx is the name of the attribute and yyy specifies the data type of the attribute.

&nbsp;&nbsp;&nbsp;&nbsp;Here is an example of an XML element with an attribute:

```xml
<lastname lang="EN">Smith</lastname>
```

&nbsp;&nbsp;&nbsp;&nbsp;The corresponding attribute definition is:

```xsd
<xs:attribute name="lang" type="xs:string"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;Attributes may have a default value OR a fixed value specified. A default value is automatically assigned to the attribute when no other value is specified. A fixed value is also automatically assigned to the attribute, and you cannot specify another value.

- In the following example the default value is "EN":

```xml
<xs:attribute name="lang" type="xs:string" default="EN"/>
```

- In the following example the fixed value is "EN":

```xml
<xs:attribute name="lang" type="xs:string" fixed="EN"/>
```

&nbsp;&nbsp;&nbsp;&nbsp;Attributes are optional by default. To specify that the attribute is required, use the "use" attribute:

```xsd
<xs:attribute name="lang" type="xs:string" use="required"/>
```

### Restrictions on Content

&nbsp;&nbsp;&nbsp;&nbsp;Restrictions are used to define acceptable values for XML elements or attributes. **When an XML element or attribute has a data type defined, it puts restrictions on the element's or attribute's content.** If an XML element is of type `xs:date` and contains a string like "Hello World", the element will not validate. With XML Schemas, you can also add your own restrictions to your XML elements and attributes. **Restrictions on XML elements are called facets.**

#### Restrictions on Values

&nbsp;&nbsp;&nbsp;&nbsp;The following example defines an element called "age" with a restriction. The value of age cannot be lower than 0 or greater than 120:

```xsd
<xs:element name="age">
  <xs:simpleType>
    <xs:restriction base="xs:integer">
      <xs:minInclusive value="0"/>
      <xs:maxInclusive value="120"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on a Set of Values

&nbsp;&nbsp;&nbsp;&nbsp;To limit the content of an XML element to a set of acceptable values, we would use the enumeration constraint. The example below defines an element called "car" with a restriction. The only acceptable values are: Audi, Golf, BMW::

```xsd
<xs:element name="car">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:enumeration value="Audi"/>
      <xs:enumeration value="Golf"/>
      <xs:enumeration value="BMW"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on a Set of Values

&nbsp;&nbsp;&nbsp;&nbsp;To limit the content of an XML element to a set of acceptable values, we would use the enumeration constraint. The example below defines an element called "car" with a restriction. The only acceptable values are: Audi, Golf, BMW:

```xsd
<xs:element name="car">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:enumeration value="Audi"/>
      <xs:enumeration value="Golf"/>
      <xs:enumeration value="BMW"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example above could also have been written like below; In this case the type "carType" can be used by other elements because it is not a part of the "car" element:

```xsd
<xs:element name="car" type="carType"/>

<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>
```

#### Restrictions on a Series of Values

&nbsp;&nbsp;&nbsp;&nbsp;To limit the content of an XML element to define a series of numbers or letters that can be used, we would use the pattern constraint. The example below defines an element called "initials" with a restriction. The only acceptable value is THREE of the LOWERCASE OR UPPERCASE letters from a to z:

```xsd
<xs:element name="initials">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[a-zA-Z][a-zA-Z][a-zA-Z]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The next example defines an element called "choice" with a restriction. The only acceptable value is ONE of the following letters: x, y, OR z:

```xsd
<xs:element name="choice">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[xyz]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example below defines an element called "letter" with a restriction. The acceptable value is zero or more occurrences of lowercase letters from a to z:

```xsd
<xs:element name="letter">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="([a-z])*"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The next example also defines an element called "letter" with a restriction. The acceptable value is one or more pairs of letters, each pair consisting of a lower case letter followed by an upper case letter. For example, "sToP" will be validated by this pattern, but not "Stop" or "STOP" or "stop":

```xsd
<xs:element name="letter">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="([a-z][A-Z])+"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;TThe next example defines an element called "gender" with a restriction. The only acceptable value is male OR female:

```xsd
<xs:element name="gender">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="male|female"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The next example defines an element called "password" with a restriction. There must be exactly eight characters in a row and those characters must be lowercase or uppercase letters from a to z, or a number from 0 to 9:

```xsd
<xs:element name="password">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[a-zA-Z0-9]{8}"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on Whitespace Characters

&nbsp;&nbsp;&nbsp;&nbsp;To specify how whitespace characters should be handled, we would use the whiteSpace constraint. This example defines an element called "address" with a restriction. The whiteSpace constraint is set to "preserve", which means that the XML processor WILL NOT remove any white space characters:

```xsd
<xs:element name="address">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:whiteSpace value="preserve"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;This example also defines an element called "address" with a restriction. The whiteSpace constraint is set to "replace", which means that the XML processor WILL REPLACE all white space characters (line feeds, tabs, spaces, and carriage returns) with spaces:

```xsd
<xs:element name="address">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:whiteSpace value="replace"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;This example also defines an element called "address" with a restriction. The whiteSpace constraint is set to "collapse", which means that the XML processor WILL REMOVE all white space characters (line feeds, tabs, spaces, carriage returns are replaced with spaces, leading and trailing spaces are removed, and multiple spaces are reduced to a single space):

```xsd
<xs:element name="address">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:whiteSpace value="collapse"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on Length

&nbsp;&nbsp;&nbsp;&nbsp;To limit the length of a value in an element, we would use the length, maxLength, and minLength constraints. This example defines an element called "password" with a restriction. The value must be exactly eight characters:

```xsd
<xs:element name="password">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:length value="8"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;This example defines another element called "password" with a restriction. The value must be minimum five characters and maximum eight characters:

```xsd
<xs:element name="password">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:minLength value="5"/>
      <xs:maxLength value="8"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions for Datatypes

| Constraint     | Description                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------- |
| enumeration    | Defines a list of acceptable values                                                                     |
| fractionDigits | Specifies the maximum number of decimal places allowed. Must be equal to or greater than zero           |
| length         | Specifies the exact number of characters or list items allowed. Must be equal to or greater than zero   |
| maxExclusive   | Specifies the upper bounds for numeric values (the value must be less than this value)                  |
| maxInclusive   | Specifies the upper bounds for numeric values (the value must be less than or equal to this value)      |
| maxLength      | Specifies the maximum number of characters or list items allowed. Must be equal to or greater than zero |
| minExclusive   | Specifies the lower bounds for numeric values (the value must be greater than this value)               |
| minInclusive   | Specifies the lower bounds for numeric values (the value must be greater than or equal to this value)   |
| minLength      | Specifies the minimum number of characters or list items allowed. Must be equal to or greater than zero |
| pattern        | Defines the exact sequence of characters that are acceptable                                            |
| totalDigits    | Specifies the exact number of digits allowed. Must be greater than zero                                 |
| whiteSpace     | Specifies how white space (line feeds, tabs, spaces, and carriage returns) is handled                   |

### XSD Complex Elements

&nbsp;&nbsp;&nbsp;&nbsp;**A complex element is an XML element that contains other elements and/or attributes.** There are four kinds of complex elements; Each of these elements may contain attributes as well:

- empty elements
- elements that contain only other elements
- elements that contain only text
- elements that contain both other elements and text:

#### XSD Empty Elements

&nbsp;&nbsp;&nbsp;&nbsp;An empty complex element cannot have contents, only attributes. A complex XML element, "product", which is empty:

```xml
<product pid="1345"/>
```

&nbsp;&nbsp;&nbsp;&nbsp; The "product" element above has no content at all. It is possible to declare the "product" element more compactly, like this:

```xsd
<xs:element name="product">
  <xs:complexType>
    <xs:attribute name="prodid" type="xs:positiveInteger"/>
  </xs:complexType>
</xs:element>
```

#### XSD Text-Only Elements

&nbsp;&nbsp;&nbsp;&nbsp;A complex text-only element can contain only simple content (text and attributes).Here is an example of an XML element, "shoesize", that contains text-only:

```xml
<shoesize country="france">35</shoesize>
```

&nbsp;&nbsp;&nbsp;&nbsp;The following example declares a complexType, "shoesize". The content is defined as an integer value, and the "shoesize" element also contains an attribute named "country". The extension element is used to expand the base simple type for the element:

```xsd
<xs:element name="shoesize">
  <xs:complexType>
    <xs:simpleContent>
      <xs:extension base="xs:integer">
        <xs:attribute name="country" type="xs:string" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
</xs:element>
```

#### XSD Elements Only

&nbsp;&nbsp;&nbsp;&nbsp;An "elements-only" complex type contains an element that contains only other elements. An XML element, "person", that contains only other elements:

```xsd
<person>
  <firstname>John</firstname>
  <lastname>Smith</lastname>
</person>
```

&nbsp;&nbsp;&nbsp;&nbsp;You can define the "person" element in a schema, like this:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;Notice the `<xs:sequence>` tag. It means that the elements defined ("firstname" and "lastname") must appear in that order inside a "person" element.

#### XSD Mixed Content

&nbsp;&nbsp;&nbsp;&nbsp;A mixed complex type element can contain attributes, elements, and text. An XML element, "letter", that contains both text and other elements:

```xsd
<letter>
  Dear Mr. <name>John Smith</name>.
  Your order <orderid>1032</orderid>
  will be shipped on <shipdate>2001-07-13</shipdate>.
</letter>
```

&nbsp;&nbsp;&nbsp;&nbsp;The following schema declares the "letter" element:

```xsd
<xs:element name="letter">
  <xs:complexType mixed="true">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
      <xs:element name="orderid" type="xs:positiveInteger"/>
      <xs:element name="shipdate" type="xs:date"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;To enable character data to appear between the child-elements of "letter", the mixed attribute must be set to "true". The `<xs:sequence>` tag means that the elements defined (name, orderid and shipdate) must appear in that order inside a "letter" element.

#### Base a complex type on an existing complex type

&nbsp;&nbsp;&nbsp;&nbsp;Look at this complex XML element, "employee", which contains only other elements:

```xsd
<employee>
  <firstname>John</firstname>
  <lastname>Smith</lastname>
</employee>
```

&nbsp;&nbsp;&nbsp;&nbsp;We can define a complex element in an XML Schema like:

```xsd
<xs:element name="employee" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

&nbsp;&nbsp;&nbsp;&nbsp;We can base a complex type on an existing complex type and add some elements, like this:

```xsd
<xs:element name="employee" type="fullpersoninfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>

<xs:complexType name="fullpersoninfo">
  <xs:complexContent>
    <xs:extension base="personinfo">
      <xs:sequence>
        <xs:element name="address" type="xs:string"/>
        <xs:element name="city" type="xs:string"/>
        <xs:element name="country" type="xs:string"/>
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```

### XSD Indicators

&nbsp;&nbsp;&nbsp;&nbsp;We can control HOW elements are to be used in documents with indicators. There are seven indicators:

- Order indicators:

  - All
  - Choice
  - Sequence

- Occurrence indicators:

  - maxOccurs
  - minOccurs

- Group indicators:
  - Group name
  - attributeGroup name

#### Order Indicators

&nbsp;&nbsp;&nbsp;&nbsp;Order indicators are used to define the order of the elements. **The `<all>` indicator specifies that the child elements can appear in any order, and that each child element must occur only once**:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:all>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:all>
  </xs:complexType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;When using the `<all>` indicator you can set the `<minOccurs>` indicator to 0 or 1 and the `<maxOccurs>` indicator can only be set to 1. **The `<choice>` indicator specifies that either one child element or another can occur**:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:choice>
      <xs:element name="employee" type="employee"/>
      <xs:element name="member" type="member"/>
    </xs:choice>
  </xs:complexType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;**The `<sequence>` indicator specifies that the child elements must appear in a specific order**:

```xsd
<xs:element name="person">
   <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

#### Occurrence Indicators

&nbsp;&nbsp;&nbsp;&nbsp;Occurrence indicators are used to define how often an element can occur. **The `<maxOccurs>` indicator specifies the maximum number of times an element can occur**:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="full_name" type="xs:string"/>
      <xs:element name="child_name" type="xs:string" maxOccurs="10"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example above indicates that the "child_name" element can occur a minimum of one time (the default value for minOccurs is 1) and a maximum of ten times in the "person" element. **The `<minOccurs>` indicator specifies the minimum number of times an element can occur**:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="full_name" type="xs:string"/>
      <xs:element name="child_name" type="xs:string"
      maxOccurs="10" minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example above indicates that the "child_name" element can occur a minimum of zero times and a maximum of ten times in the "person" element.

&nbsp;&nbsp;&nbsp;&nbsp;For all "Order" and "Group" indicators (any, all, choice, sequence, group name, and group reference) the default value for maxOccurs and minOccurs is 1. To allow an element to appear an unlimited number of times, use the maxOccurs="unbounded" statement.

#### Group Indicators

&nbsp;&nbsp;&nbsp;&nbsp;**Group indicators are used to define related sets of elements.** Element groups are defined with the group declaration, like this:

```xsd
<xs:group name="groupname">
...
</xs:group>
```

&nbsp;&nbsp;&nbsp;&nbsp;You must define an all, choice, or sequence element inside the group declaration. The following example defines a group named "persongroup", that defines a group of elements that must occur in an exact sequence:

```xsd
<xs:group name="persongroup">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
    <xs:element name="birthday" type="xs:date"/>
  </xs:sequence>
</xs:group>
```

&nbsp;&nbsp;&nbsp;&nbsp;After you have defined a group, you can reference it in another definition, like this:

```xsd
<xs:element name="person" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:group ref="persongroup"/>
    <xs:element name="country" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

&nbsp;&nbsp;&nbsp;&nbsp;Attribute groups are defined with the attributeGroup declaration, like this:

```xsd
<xs:attributeGroup name="groupname">
...
</xs:attributeGroup>
```

&nbsp;&nbsp;&nbsp;&nbsp;The following example defines an attribute group named "personattrgroup":

```xsd
<xs:attributeGroup name="personattrgroup">
  <xs:attribute name="firstname" type="xs:string"/>
  <xs:attribute name="lastname" type="xs:string"/>
  <xs:attribute name="birthday" type="xs:date"/>
</xs:attributeGroup>
```

&nbsp;&nbsp;&nbsp;&nbsp;After you have defined an attribute group, you can reference it in another definition, like this:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:attributeGroup ref="personattrgroup"/>
  </xs:complexType>
</xs:element>
```

### `<any>` and `<anyAttribute>`

&nbsp;&nbsp;&nbsp;&nbsp;The `<any>` and `<anyAttribute>` elements are used to make EXTENSIBLE documents! They allow documents to contain additional elements that are not declared in the main XML schema.

#### XSD The `<any>` Element

&nbsp;&nbsp;&nbsp;&nbsp;The `<any>` element enables us to extend the XML document with elements not specified by the schema. The following example is a fragment from an XML schema called "family.xsd". It shows a declaration for the "person" element. By using the `<any>` element we can extend (after `<lastname>`) the content of "person" with any element:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
      <xs:any minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

#### XSD The `<anyAttribute>` Element

&nbsp;&nbsp;&nbsp;&nbsp;The `<anyAttribute>` element enables us to extend the XML document with attributes not specified by the schema. The following example is a fragment from an XML schema called "family.xsd". It shows a declaration for the "person" element. By using the `<anyAttribute>` element we can add any number of attributes to the "person" element:

```xsd
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
    <xs:anyAttribute/>
  </xs:complexType>
</xs:element>
```

## XML Web Services

&nbsp;&nbsp;&nbsp;&nbsp;Web services communicate using open protocols. By using Web services, your application can publish its function or message to the rest of the world. Web services use XML to code and to decode data, and SOAP to transport it (using open protocols).With Web services you can exchange data between different applications and different platforms.

&nbsp;&nbsp;&nbsp;&nbsp;Before you learn about these web services you should have a basic understanding of XML and XML Namespaces.

### WSDL

&nbsp;&nbsp;&nbsp;&nbsp;WSDL stands for Web Services Description Language. WSDL is an XML-based language for describing Web services.

#### WSDL Documents

&nbsp;&nbsp;&nbsp;&nbsp;An WSDL document describes a web service. It specifies the location of the service, and the methods of the service, using these major elements:

| Element      | Description                                                               |
| ------------ | ------------------------------------------------------------------------- |
| `<types>`    | Defines the (XML Schema) data types used by the web service               |
| `<message>`  | Defines the data elements for each operation                              |
| `<portType>` | Describes the operations that can be performed and the messages involved. |
| `<binding>`  | Defines the protocol and data format for each port type                   |

&nbsp;&nbsp;&nbsp;&nbsp;The main structure of a WSDL document looks like this:

```xml
<definitions>

<types>
  data type definitions........
</types>

<message>
  definition of the data being communicated....
</message>

<portType>
  set of operations......
</portType>

<binding>
  protocol and data format specification....
</binding>

</definitions>
```

&nbsp;&nbsp;&nbsp;&nbsp;This is a simplified fraction of a WSDL document:

```xml
<message name="getTermRequest">
  <part name="term" type="xs:string"/>
</message>

<message name="getTermResponse">
  <part name="value" type="xs:string"/>
</message>

<portType name="glossaryTerms">
  <operation name="getTerm">
    <input message="getTermRequest"/>
    <output message="getTermResponse"/>
  </operation>
</portType>
```

&nbsp;&nbsp;&nbsp;&nbsp;**The `<portType>` element defines a web service, the operations that can be performed, and the messages that are involved.** In this example the `<portType>` element defines "glossaryTerms" as the name of a port, and "getTerm" as the name of an operation. The "getTerm" operation has an input message called "getTermRequest" and an output message called "getTermResponse". The `<message>` elements define the parts of each message and the associated data types. The "getTerm" operation requires an input message called "getTermRequest" with a parameter called "term", and will return an output message called "getTermResponse" with a parameter called "value".

### SOAP

&nbsp;&nbsp;&nbsp;&nbsp;SOAP stands for Simple Object Access Protocol. SOAP is an XML based format for sending and receiving messages. It is important for web applications to be able to communicate over the Internet. The best way to communicate between applications is over HTTP, because HTTP is supported by all Internet browsers and servers. SOAP was created to accomplish this. SOAP provides a way to communicate between applications running on different operating systems, with different technologies and programming languages.

#### SOAP Building Blocks

&nbsp;&nbsp;&nbsp;&nbsp;A SOAP message is an ordinary XML document containing the following elements:

- An **Envelope** element that identifies the XML document as a SOAP message
- A **Header** element that contains header information
- A **Body** element that contains call and response information
- A **Fault** element containing errors and status information

&nbsp;&nbsp;&nbsp;&nbsp;All the elements above are declared in the default namespace for the SOAP envelope: `http://www.w3.org/2003/05/soap-envelope/` and the default namespace for SOAP encoding and data types is: `http://www.w3.org/2003/05/soap-encoding`.

```xml
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Header>
...
</soap:Header>

<soap:Body>
...
  <soap:Fault>
  ...
  </soap:Fault>
</soap:Body>

</soap:Envelope>
```

##### The SOAP Envelope Element

&nbsp;&nbsp;&nbsp;&nbsp;The required SOAP Envelope element is the root element of a SOAP message. This element defines the XML document as a SOAP message.

```xml
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">
  ...
  Message information goes here
  ...
</soap:Envelope>
```

##### The `xmlns:soap` Namespace

&nbsp;&nbsp;&nbsp;&nbsp;Notice the `xmlns:soap` namespace in the example above. It should always have the value of: `http://www.w3.org/2003/05/soap-envelope/`. **The namespace defines the Envelope as a SOAP Envelope.** If a different namespace is used, the application generates an error and discards the message.

##### The encodingStyle Attribute

&nbsp;&nbsp;&nbsp;&nbsp;**The encodingStyle attribute is used to define the data types used in the document.** This attribute may appear on any SOAP element, and applies to the element's contents and all child elements.

##### The SOAP Header Element

&nbsp;&nbsp;&nbsp;&nbsp;The optional SOAP Header element contains application-specific information (like authentication, payment, etc) about the SOAP message. If the Header element is present, it must be the first child element of the Envelope element. All immediate child elements of the Header element must be namespace-qualified.

```xml
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Header>
  <m:Trans xmlns:m="https://www.w3schools.com/transaction/"
  soap:mustUnderstand="1">234
  </m:Trans>
</soap:Header>
...
...
</soap:Envelope>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example above contains a header with a "Trans" element, a "mustUnderstand" attribute with a value of 1, and a value of 234.

&nbsp;&nbsp;&nbsp;&nbsp;SOAP defines three attributes in the default namespace. These attributes are: mustUnderstand, actor, and encodingStyle. The attributes defined in the SOAP Header defines how a recipient should process the SOAP message.

##### The mustUnderstand Attribute

&nbsp;&nbsp;&nbsp;&nbsp;The SOAP mustUnderstand attribute can be used to indicate whether a header entry is mandatory or optional for the recipient to process. If you add mustUnderstand="1" to a child element of the Header element it indicates that the receiver processing the Header must recognize the element. If the receiver does not recognize the element it will fail when processing the Header.

##### The actor Attribute

&nbsp;&nbsp;&nbsp;&nbsp;A SOAP message may travel from a sender to a receiver by passing different endpoints along the message path. However, not all parts of a SOAP message may be intended for the ultimate endpoint, instead, it may be intended for one or more of the endpoints on the message path. The SOAP actor attribute is used to address the Header element to a specific endpoint.

```xml
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Header>
  <m:Trans xmlns:m="https://www.w3schools.com/transaction/"
  soap:actor="https://www.w3schools.com/code/">234
  </m:Trans>
</soap:Header>
...
...
</soap:Envelope>
```

##### The SOAP Body Element

&nbsp;&nbsp;&nbsp;&nbsp;The required SOAP Body element contains the actual SOAP message intended for the ultimate endpoint of the message. Immediate child elements of the SOAP Body element may be namespace-qualified.

```xml
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Body>
  <m:GetPrice xmlns:m="https://www.w3schools.com/prices">
    <m:Item>Apples</m:Item>
  </m:GetPrice>
</soap:Body>

</soap:Envelope>
```

&nbsp;&nbsp;&nbsp;&nbsp;The example above requests the price of apples. Note that the m:GetPrice and the Item elements above are application-specific elements. They are not a part of the SOAP namespace. A SOAP response could look something like this:

```xml
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Body>
  <m:GetPriceResponse xmlns:m="https://www.w3schools.com/prices">
    <m:Price>1.90</m:Price>
  </m:GetPriceResponse>
</soap:Body>

</soap:Envelope>
```

##### The SOAP Fault Element

&nbsp;&nbsp;&nbsp;&nbsp;The optional SOAP Fault element is used to indicate error messages. The SOAP Fault element holds errors and status information for a SOAP message. If a Fault element is present, it must appear as a child element of the Body element. A Fault element can only appear once in a SOAP message. The SOAP Fault element has the following sub elements:

| Sub Element     | Description                                                              |
| --------------- | ------------------------------------------------------------------------ |
| `<faultcode>`   | A code for identifying the fault                                         |
| `<faultstring>` | A human readable explanation of the fault                                |
| `<faultactor>`  | Information about who caused the fault to happen                         |
| `<detail>`      | Holds application specific error information related to the Body element |

##### SOAP Fault Codes

&nbsp;&nbsp;&nbsp;&nbsp;The faultcode values defined below must be used in the faultcode element when describing faults:

| Error           | Description                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------ |
| VersionMismatch | Found an invalid namespace for the SOAP Envelope element                                                           |
| MustUnderstand  | An immediate child element of the Header element, with the mustUnderstand attribute set to "1", was not understood |
| Client          | The message was incorrectly formed or contained incorrect information                                              |
| Server          | There was a problem with the server so the message could not proceed                                               |

#### SOAP Binding

&nbsp;&nbsp;&nbsp;&nbsp;The SOAP specification defines the structure of the SOAP messages, not how they are exchanged. This gap is filled by what is called "SOAP Bindings". SOAP bindings are mechanisms which allow SOAP messages to be effectively exchanged using a transport protocol.

&nbsp;&nbsp;&nbsp;&nbsp;Most SOAP implementations provide bindings for common transport protocols, such as HTTP or SMTP. HTTP is synchronous and widely used. A SOAP HTTP request specifies at least two HTTP headers: Content-Type and Content-Length.

##### Content-Type

&nbsp;&nbsp;&nbsp;&nbsp;The Content-Type header for a SOAP request and response defines the MIME type for the message and the character encoding (optional) used for the XML body of the request or response.

##### Content-Length

&nbsp;&nbsp;&nbsp;&nbsp;The Content-Length header for a SOAP request and response specifies the number of bytes in the body of the request or response.

#### WSDL Binding to SOAP

&nbsp;&nbsp;&nbsp;&nbsp;WSDL bindings defines the message format and protocol details for a web service. A request-response operation example:

```xml
<message name="getTermRequest">
  <part name="term" type="xs:string"/>
</message>

<message name="getTermResponse">
  <part name="value" type="xs:string"/>
</message>

<portType name="glossaryTerms">
  <operation name="getTerm">
    <input message="getTermRequest"/>
    <output message="getTermResponse"/>
  </operation>
</portType>

<binding type="glossaryTerms" name="b1">
   <soap:binding style="document"
   transport="http://schemas.xmlsoap.org/soap/http" />
   <operation>
     <soap:operation soapAction="http://example.com/getTerm"/>
     <input><soap:body use="literal"/></input>
     <output><soap:body use="literal"/></output>
  </operation>
</binding>
```

- The **binding** element has two attributes - name and type. The name attribute (you can use any name you want) defines the name of the binding, and the type attribute points to the port for the binding, in this case the "glossaryTerms" port.
- The **soap:binding** element has two attributes - style and transport. The style attribute can be "rpc" or "document". In this case we use document. The transport attribute defines the SOAP protocol to use. In this case we use HTTP.
- The **operation** element defines each operation that the portType exposes. For each operation the corresponding SOAP action has to be defined. You must also specify how the input and output are encoded. In this case we use "literal".

### RSS

&nbsp;&nbsp;&nbsp;&nbsp;With RSS it is possible to distribute up-to-date web content from one web site to thousands of other web sites around the world. RSS stands for Really Simple Syndication. RSS allows you to syndicate your site content. It defines an easy way to share and view headlines and content.

&nbsp;&nbsp;&nbsp;&nbsp;RSS was designed to show selected data. Without RSS, users will have to check your site daily for new updates. This may be too time-consuming for many users. With an RSS feed (RSS is often called a News feed or RSS feed) they can check your site faster using an RSS aggregator (a site or program that gathers and sorts out RSS feeds). Since RSS data is small and fast-loading, it can easily be used with services like cell phones or PDA's.Web-rings with similar information can easily share data on their web sites to make them better and more useful.

#### How RSS Works

&nbsp;&nbsp;&nbsp;&nbsp;RSS is used to share content between websites. With RSS, you register your content with companies called aggregators. So, to be a part of it:

- First, create an RSS document and save it with an .xml extension.
- Then, upload the file to your website.
- Next, register with an RSS aggregator.

&nbsp;&nbsp;&nbsp;&nbsp;Each day the aggregator searches the registered websites for RSS documents, verifies the link, and displays information about the feed so clients can link to documents that interests them.

#### RSS Example

&nbsp;&nbsp;&nbsp;&nbsp;RSS documents use a self-describing and simple syntax. Here is a simple RSS document:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">

<channel>
  <title>W3Schools Home Page</title>
  <link>https://www.w3schools.com</link>
  <description>Free web building tutorials</description>
  <item>
    <title>RSS Tutorial</title>
    <link>https://www.w3schools.com/xml/xml_rss.asp</link>
    <description>New RSS tutorial on W3Schools</description>
  </item>
  <item>
    <title>XML Tutorial</title>
    <link>https://www.w3schools.com/xml</link>
    <description>New XML tutorial on W3Schools</description>
  </item>
</channel>

</rss>
```

- The first line in the document - the XML declaration - defines the XML version and the character encoding used in the document. In this case the document conforms to the 1.0 specification of XML and uses the UTF-8 character set.
- The next line is the RSS declaration which identifies that this is an RSS document (in this case, RSS version 2.0).
- **The next line contains the `<channel>` element. This element is used to describe the RSS feed.**
- The `<channel>` element has three required child elements:

  - `<title>` - Defines the title of the channel (e.g. W3Schools Home Page)
  - `<link>` - Defines the hyperlink to the channel (e.g. https://www.w3schools.com)
  - `<description>` - Describes the channel (e.g. Free web building tutorials)

- Each `<channel>` element can have one or more `<item>` elements. **Each `<item>` element defines an article or "story" in the RSS feed.**
- The `<item>` element has three required child elements:

  - `<title>` - Defines the title of the item (e.g. RSS Tutorial)
  - `<link>` - Defines the hyperlink to the item (e.g. https://www.w3schools.com/xml/xml_rss.asp)
  - `<description>` - Describes the item (e.g. New RSS tutorial on W3Schools)

- Finally, the two last lines close the `<channel>` and `<rss>` elements.

#### RSS Readers

&nbsp;&nbsp;&nbsp;&nbsp;An RSS Reader is used to read RSS Feeds! RSS readers are available for many different devices and OS. There are a lot of different RSS readers. Some work as web services, and some are limited to windows (or Mac, PDA or UNIX):

- **QuiteRSS** - An open-source, cross-platform RSS/Atom news feed reader
- **FeedReader** - A simple, straightforward feed reader that easily handles large number of feeds
- Most browsers have a built-in RSS Reader.

---

## Where can you dig more?

&nbsp;&nbsp;&nbsp;&nbsp;There is a lot of useful information about XML present on the internet. But some of the interesting resources which you should definitely visit are given below:

- [XML Tutorial](https://www.w3schools.com/xml/) by w3schools.com
- [Using XML](https://alistapart.com/article/usingxml/) by J. David Eisenberg
- [Introduction to the Annotated XML Specification](https://www.xml.com/axml/axml.html) by Tim Bray

```

```
