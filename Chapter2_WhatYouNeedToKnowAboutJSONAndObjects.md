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
