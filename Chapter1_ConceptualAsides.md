## Chapter 1

# Conceptual Asides

&nbsp;&nbsp;&nbsp;&nbsp;For a long time, I kept myself away from the adventurous and thrilling world of Integrations. However, integration is actually a very simple concept and it is so much fun to do. And ServiceNow is a great tool when it comes to integrating with other tools.

&nbsp;&nbsp;&nbsp;&nbsp;ServiceNow community have many great people around the globe, who not only did lot of crazy stuff but also helped many many others like me to understand these concepts. Also ServiceNow itself has a great amount of resources, learning paths, courses and well-structured documentation that you can take advantage of. But sometimes it can be difficult to read and understand all this tech terms of official documentations, And it can be very easy if they are consolidated at one place with practical use cases. Which is exactly the journey I will be taking you all on. Whatever you are going to learn in this journey is not something I came up with, It is already there! But what we will be doing is connecting the dots, going step by step through each concept building on previous ones. In other words, I am going to teach you "How to read the docs", but I promise by end of all these chapters, you will be able to build almost any integration in the world; though I'm going to restrict myself to ServiceNow platform, when explaining all those stuff.

&nbsp;&nbsp;&nbsp;&nbsp;Well, That's a big committement! and in order to make it true, we need to think of some concepts that are essential to understand before we actually dig deeper. Don't worry, we'll go pretty quick through them in this chapter and touch them back once we actually do the tech part.

## What is API

&nbsp;&nbsp;&nbsp;&nbsp;When you chat with a friend, you need a mobile (or in other words, a communication device) to do that. Or in order to open a door you need a handle. Application Programming Interface or API is a similar concept, and it helps two programs to communicate & enable access a resource with each other.

&nbsp;&nbsp;&nbsp;&nbsp;Let us try to understand this another way. Think that you are hungry and want to eat a pizza. You go to the nearest restaurant, check the menu and make the order to the waiter. Waiter in turn takes the order to the kitchen, brings the pizza from the kitchen and deliver the pizza to your table. The waiter plays the similar part as of the API.

&nbsp;&nbsp;&nbsp;&nbsp; In IT world, Client application makes an request to the Server and recieves the response back. API is a mid layer that handles this communication.

![What is API](/images/Chapter1_1.png)

## What is REST API

&nbsp;&nbsp;&nbsp;&nbsp;Representational state transfer or REST is the most popular approach of building APIs. When a request for data is sent to a REST API, it’s usually done through hypertext transfer protocol (HTTP). Once a request is received, APIs designed for REST can return messages in a variety of formats: HTML, XML, plain text, and JSON.

#### A request is made up of four things:

- The Endpoint
- The method
- The headers
- The body

## The Endpoint

&nbsp;&nbsp;&nbsp;&nbsp;The endpoint is the url you request for. It generally consists of base path and resource path.

```js
https://dev124645.service-now.com/api/now/table/incident
```

## The method

#### POST: Create

&nbsp;&nbsp;&nbsp;&nbsp;POST method is used to submit the information to the server.

#### GET: Read

&nbsp;&nbsp;&nbsp;&nbsp;GET method is the most common of all the request methods. It is used to fetch the desired resource from the server.

#### PUT/PATCH: Update

&nbsp;&nbsp;&nbsp;&nbsp;Both PUT & PATCH are used to modify the resources on the server with a slight difference. PUT is a method of modifying resource where the client sends data that updates the entire resource. PATCH is a method of modifying resources where the client sends partial data that is to be updated without modifying the entire data.

#### DELETE: Delete

&nbsp;&nbsp;&nbsp;&nbsp;POST method is used to delete the resource identified by the request url.

## HTTP Headers

&nbsp;&nbsp;&nbsp;&nbsp;Client and Server can pass the extra bit of information with the request and response using HTTP headers.

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

&nbsp;&nbsp;&nbsp;&nbsp;Used to pass credentials so that server can authenticate.

#### Access-Control-Allow-Origin

&nbsp;&nbsp;&nbsp;&nbsp;Specifies which origin is allowed to access the resources.

#### Access-Control-Allow-Methods

&nbsp;&nbsp;&nbsp;&nbsp;Specifies which methods are allowed to access the resources.

##

&nbsp;&nbsp;&nbsp;&nbsp;

##

&nbsp;&nbsp;&nbsp;&nbsp;
