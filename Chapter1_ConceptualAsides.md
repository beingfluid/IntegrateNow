## Chapter 1

# Conceptual Asides

&nbsp;&nbsp;&nbsp;&nbsp;For a long time, I kept myself away from the adventurous and thrilling world of Integrations. However, integration is actually a very simple concept and it is so much fun to do. And ServiceNow is a great tool when it comes to integrating with other tools.

&nbsp;&nbsp;&nbsp;&nbsp;ServiceNow community have many great people around the globe, who not only did lot of crazy stuff but also helped many many others like me to understand these concepts. Also ServiceNow itself has a great amount of resources, learning paths, courses and well-structured documentation that you can take advantage of. But sometimes it can be difficult to read and understand all this tech terms of official documentations, And it can be very easy if they are consolidated at one place with practical use cases. Which is exactly the journey I will be taking you all on. Whatever you are going to learn in this journey is not something I came up with, It is already there! But what we will be doing is connecting the dots, going step by step through each concept building on previous ones. In other words, I am going to teach you "How to read the docs", but I promise by end of all these chapters, you will be able to build almost any integration in the world; though I'm going to restrict myself to ServiceNow platform, when explaining all those stuff.

&nbsp;&nbsp;&nbsp;&nbsp;Well, That's a big committement! and in order to make it true, we need to think of some concepts that are essential to understand before we actually dig deeper. Don't worry, we'll go pretty quick through them in this chapter and touch them back once we actually do the tech part.

## What is API

&nbsp;&nbsp;&nbsp;&nbsp;When you chat with a friend, you need a mobile (or in other words, a communication device) to do that. Or in order to open a door you need a handle. Application Programming Interface or API is a similar concept, and it helps two programs to communicate & enable exchange of information with each other.

&nbsp;&nbsp;&nbsp;&nbsp;Let us try to understand this another way. Think that you are hungry and want to eat a pizza. You go to the nearest restaurant, check the menu and make the order to the waiter. Waiter in turn takes the order to the kitchen, brings the pizza from the kitchen and deliver the pizza to your table. The waiter plays the similar part as of the API.

&nbsp;&nbsp;&nbsp;&nbsp; In IT world, Client application requests information from a server. A server processes the request and returns a status code and a response body. When the response body is returned, the Client extracts information from the response body and takes action on the extracted data. API is a mid layer that handles this communication. Scripted REST Services allow developers to create their own APIs on the ServiceNow Platform.

![What is API](/images/Chapter1_1.png)

## What is REST API

&nbsp;&nbsp;&nbsp;&nbsp;Representational state transfer or REST is the most popular approach of building APIs. When a request for data is sent to a REST API, it’s usually done through hypertext transfer protocol (HTTP). Once a request is received, APIs designed for REST can return messages in a variety of formats: HTML, XML, plain text, and JSON.

#### A request is made up of four things:

- The Endpoint
- The method
- The headers
- The body

## The Endpoint

&nbsp;&nbsp;&nbsp;&nbsp;The endpoint is the url you request for. It generally consists of base path and resource path. E.g.

```js
https://dev124645.service-now.com/api/now/table/incident
```

&nbsp;&nbsp;&nbsp;&nbsp;Every web service provider will have the API documentation and that needs to be referenced in order to configure the HTTP method endpoint.

## The method

&nbsp;&nbsp;&nbsp;&nbsp;HTTP methods define the action to take for a resource, such as retrieving information or updating a record. The available HTTP Methods are:

#### POST: Create

&nbsp;&nbsp;&nbsp;&nbsp;POST method is used to submit the information to the server.

#### GET: Read

&nbsp;&nbsp;&nbsp;&nbsp;GET method is the most common of all the request methods. It is used to fetch the desired resource from the server.

#### PUT/PATCH: Update

&nbsp;&nbsp;&nbsp;&nbsp;Both PUT & PATCH are used to modify the resources on the server with a slight difference. PUT is a method of modifying resource where the client sends data that updates the entire resource. PATCH is a method of modifying resources where the client sends partial data that is to be updated without modifying the entire data.

#### DELETE: Delete

&nbsp;&nbsp;&nbsp;&nbsp;POST method is used to delete the resource identified by the request url.

## HTTP Headers

&nbsp;&nbsp;&nbsp;&nbsp;Client and Server can pass the extra bit of information with the request and response using HTTP headers. The Server determines which headers are supported or required.

&nbsp;&nbsp;&nbsp;&nbsp;The most widely used HTTP Headers are:

- Accept
- Content-Type
- Authorization
- Access-Control-Allow-Origin
- Access-Control-Allow-Methods

#### Accept

&nbsp;&nbsp;&nbsp;&nbsp;Type of data client can understand.

#### Content-Type

&nbsp;&nbsp;&nbsp;&nbsp;Specifies the media type of the resource.

#### Authorization

&nbsp;&nbsp;&nbsp;&nbsp;Used to pass credentials so that server can authenticate. Different web service providers may require different types of authentication.

#### Access-Control-Allow-Origin

&nbsp;&nbsp;&nbsp;&nbsp;Specifies which origin is allowed to access the resources.

#### Access-Control-Allow-Methods

&nbsp;&nbsp;&nbsp;&nbsp;Specifies which methods are allowed to access the resources.

## Accept vs. Content-Type

&nbsp;&nbsp;&nbsp;&nbsp;As we have discussed above, Accept is the type of data client can understand, whereas Content-Type specifies the media type of the resource.

&nbsp;&nbsp;&nbsp;&nbsp;What this actually means is that The Accept header is used to inform the server by the client that which content type is understandable by the client expressed as MIME-types. By using the Content-negotiation the server selects a proposal of the content type and informs the client of its choice with the Content-type response header.

&nbsp;&nbsp;&nbsp;&nbsp;I assume, almost all of you have worked in the Operations team. And you might have receieved an incident or an request from the user, who understand only french or german, while you can only speak english. Lets say, in such instances you might use some kind of translator to convert your response in user-specific language to respond to the user. Let us consider, user does the same and convert his response into english that you understand. Now if you are asking user for an input by this means, The language in which you did respond to the user (french/german) will be an Accept and the language in which you did receieve the response (i.e. english) will be a Content-Type.

&nbsp;&nbsp;&nbsp;&nbsp;Both this headers are expressed by as MIME-types. E.g.

```js
Content-Type:application/json;
```

![Accept vs Content-Type](/images/Headers.png)

## HTTP Status Codes

&nbsp;&nbsp;&nbsp;&nbsp;I'm sure you have came across the scenerio, when you tried to access a webpage and recieved an 404 (Page not found) or 403 (Access Forbidden) error? This are status codes.

&nbsp;&nbsp;&nbsp;&nbsp;Server always returns the HTTP status code with the response. The HTTP status codes refer to the interaction with the REST service provider. The status codes do not tell anything about the requested data. ServiceNow APIs return standard HTTP status codes.:

- 1xx: Informational
- 2xx: Success
- 3xx: Redirection
- 4xx: Client Error
- 5xx: Server Error

![Status Code](/images/statuscode2.png)

## HTTP Query Parameters

&nbsp;&nbsp;&nbsp;&nbsp;HTTP Query Parameters are appended to the endpoint url after '?'. The query parameters are specific to the selected API method and control what information developers using the API can pass in the API request URL.

```js
https://dev124645.service-now.com/api/now/table/incident?sysparm_query=active%3Dtrue&sysparm_limit=10

```

## Outbound vs. Inbound REST Integrations

&nbsp;&nbsp;&nbsp;&nbsp;When ServiceNow consumes a web services from third party providers and other ServiceNow instances, It is considered as a Outbound REST Integration. Whereas, In an inbound request, a third-party application requests an action through a ServiceNow API.

#### Outbound REST Integration

![Outbound](/images/app_store_learnv2_rest_sandiego_outbound_images_outbound_genericrequest.png)

#### Inbound REST Integration

![Inbound](/images/app_store_learnv2_rest_sandiego_inbound_images_inbound_genericrequest.png)

##

&nbsp;&nbsp;&nbsp;&nbsp;

## What's next?

&nbsp;&nbsp;&nbsp;&nbsp; In next chapter, we will see some of the concepts & methods related to javascript JSON and Objects, before diving into actual ServiceNow integration jungle. Knowing this simple concepts will be extermely helpful and will make us confident about the code that we are going to write. Believe me, you are going to use hell lot of JSON.
