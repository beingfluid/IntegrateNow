## Chapter 7

# RSS web service

&nbsp;&nbsp;&nbsp;&nbsp;**RSS (Rich Site Summary) is a format for delivering web-based information that changes regularly.** With RSS it is possible to distribute up-to-date web content from one web site to thousands of other web sites around the world. RSS allows you to syndicate your site content. It defines an easy way to share and view headlines and content.

&nbsp;&nbsp;&nbsp;&nbsp;RSS was designed to show selected data. Without RSS, users will have to check your site daily for new updates. This may be too time-consuming for many users. With an RSS feed (RSS is often called a News feed or RSS feed) they can check your site faster using an RSS aggregator (a site or program that gathers and sorts out RSS feeds).

## How RSS Works

&nbsp;&nbsp;&nbsp;&nbsp;RSS is used to share content between websites. With RSS, you register your content with companies called aggregators. So, to be a part of it:

- First, create an RSS document and save it with an .xml extension.
- Then, upload the file to your website.
- Next, register with an RSS aggregator.

&nbsp;&nbsp;&nbsp;&nbsp;Each day the aggregator searches the registered websites for RSS documents, verifies the link, and displays information about the feed so clients can link to documents that interests them.

## RSS feed generator

&nbsp;&nbsp;&nbsp;&nbsp;ServiceNow supports the dynamic generation of RSS feeds. Much like our Web Services implementation, the retrieval of an RSS feed representation of information is simply done by specifying an RSS parameter at the end of the URL to a table list. For example, the following will return a list of all incidents in RSS 2.0 format :

```js
https://dev124645.service-now.com/incident_list.do?&RSS
```

&nbsp;&nbsp;&nbsp;&nbsp;Replace the instance name with your own &visit the above URL, you should see the following output :

![RSS1](./images/RSS1.png)

&nbsp;&nbsp;&nbsp;&nbsp;To associate a query to the list so that a filtered list is returned, use the sysparm_query parameter. If you have a multi part query then you would separate the parts with the `^` character. For example, following will return a list of all incidents where the priority as 1 (Critical) and category as software :

```js
https://dev124645.service-now.com/incident_list.do?sysparm_query=priority=1^category=software&RSS
```

&nbsp;&nbsp;&nbsp;&nbsp;Copy and paste the above URL to your browser and replace the instance name with your own before clicking enter, you should see the following output :

![RSS2](./images/RSS2.png)

&nbsp;&nbsp;&nbsp;&nbsp;If you want to query on a field that is a reference to another file then you need to use javascript to resolve the reference to the other file. For example, the assigned_to field in incident is a reference to a user record. If you wanted to find all the incidents assigned to "ITIL User" then you would do the following:

```js
https://dev124645.service-now.com/incident.do?sysparm_query=assigned_to=javascript:GetIDValue(%27sys_user%27,%27ITIL%20User%27)&RSS
```

&nbsp;&nbsp;&nbsp;&nbsp;Replace the instance name with your own &open the URL to your browser, you should see the following output :
![RSS3](./images/RSS3.png)

&nbsp;&nbsp;&nbsp;&nbsp;You can in most cases simply append "&RSS" to a URL that you generate in the UI or that of your favorite module. The easiest way to get the URL is to simply click the last breadcrumb from the list view. After appending `&RSS` then you can use this URL in your RSS feed reader :

- Navigate to **Incident > Open**.
  ![RSS4](./images/RSS4.png)
- Right-click the end of the filter breadcrumb and select **Copy URL** from the context menu.
  ![RSS5](./images/RSS5.png)

&nbsp;&nbsp;&nbsp;&nbsp;After completing the above steps, you should have the url similar to the following copied to your clipboard:

```js
https://dev124645.service-now.com/incident_list.do?sysparm_query=active%3Dtrue&sysparm_view=
```

&nbsp;&nbsp;&nbsp;&nbsp;After appending `&RSS` our URL looks like this:

```js
https://dev124645.service-now.com/incident_list.do?sysparm_query=active%3Dtrue&sysparm_view=&RSS
```

&nbsp;&nbsp;&nbsp;&nbsp;Visit the newly constructed URL in your browser, you should see the output similar to this:
![RSS6](./images/RSS6.png)

### Limiting results with a view

&nbsp;&nbsp;&nbsp;&nbsp;The description element in the returned RSS xml is constructed using the view as specified in the URL, when no view is specified, the default no-name view is used. To change this format, specify the sysparm_view parameter on the URL. For example, the following request will return the incidents list. However, the result will be restricted to only the fields available in the ess view:

```js
https://dev124645.service-now.com/incident_list.do?sysparm_query=active%3Dtrue&sysparm_view=ess&RSS
```

![RSS7](./images/RSS7.png)

### RSS basic authentication

&nbsp;&nbsp;&nbsp;&nbsp;To enforce basic authentication on each request for an RSS feed, set the property `glide.basicauth.required.rss` to `true`. RSS request would have to contain the **Authorization** header as specified in the Authentication protocol. Because the request is non-interactive, we always require the Authorization header during a request.

&nbsp;&nbsp;&nbsp;&nbsp;To specify basic authentication on the URL, put the username and password pair separated by a colon in front of the server name before an `@` character. For example, to submit the demo credentials for the admin user, we will modify the above URL as following:

```js
https://MyAdminUserName:MyAdminPassword@dev124645.service-now.com/incident_list.do?sysparm_query=active%3Dtrue&sysparm_view=ess&RSS
```

&nbsp;&nbsp;&nbsp;&nbsp;You can visit this link in any browser or incognito tab to authenticate as admin user and generate the RSS feeds.

### RSS title override

&nbsp;&nbsp;&nbsp;&nbsp;You may optionally override the automatically generated title of the RSS feed by added the `sysparm_title` parameter to the request URL. For example, you can specify the title `Active Incidents` using the parameter `sysparm_title` as below:

```js
https://MyAdminUserName:MyAdminPassword@dev124645.service-now.com/incident_list.do?sysparm_query=active%3Dtrue&sysparm_view=ess&RSS&sysparm_title=Active Incidents
```

![RSS9](./images/RSS9.png)

## RSS Example

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

## RSS Readers

&nbsp;&nbsp;&nbsp;&nbsp;An RSS Reader is used to read RSS Feeds! RSS readers are available for many different devices and OS. There are a lot of different RSS readers. Some work as web services, and some are limited to windows (or Mac, PDA or UNIX):

- **QuiteRSS** - An open-source, cross-platform RSS/Atom news feed reader
- **FeedReader** - A simple, straightforward feed reader that easily handles large number of feeds
- Most browsers have a built-in RSS Reader.
