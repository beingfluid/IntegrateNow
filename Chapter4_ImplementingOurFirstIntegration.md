## Chapter 4 (Draft)

# Implementing Our First Integration

## A clearer picture

&nbsp;&nbsp;&nbsp;&nbsp;Till this point, we have seen what Inbound integration is in the context of ServiceNow, got familier with REST API explorer and got a faded picture of what we will be implementing in our first integration. I feel this is a perfect time to make that picture more clear. Please refer the following image:

![drawio1](./images/drawio1.png)

&nbsp;&nbsp;&nbsp;&nbsp;The above image specifies that whenever an incident is created on Vendor (Company A) instance with a specific Service and assigned to Specific group (both of them should be predefined by business), The copy of incident is created on Customer (Company B) instance and assigned to specific assignment group (also predefined by business).

&nbsp;&nbsp;&nbsp;&nbsp;So straightforward right? Well, no! When you will work on real life implementations you will notice that there is always a tweak, if not you are just lucky. Please refer the following image:

![drawio2](./images/drawio2.png)

&nbsp;&nbsp;&nbsp;&nbsp;As we can notice from the above image,our Vendor (Company A) instance has an additional On hold reason choice "Awaiting Company A Validation" (for some internal validation). Whereas our Customer (Company B) instance has all Out of the box (OOTB) choices. So our first tweak is we need to map our custom choice "Awaiting Company A Validation" from the Vendor instance to the "Awaiting Vendor" on the Customer i.e. Company B instance.

&nbsp;&nbsp;&nbsp;&nbsp;Those who are unaware about what these OOTB choices mean, you should read the answer to the community question by Mark Stanger, which can be found [here](https://community.servicenow.com/community?id=community_question&sys_id=23e90220dbc0eb805129a851ca9619f2). For ease i will replicate the original response here :

- **Awaiting Caller:** Waiting on a response back from the caller after the technician has requested additional information.
- **Awaiting Problem:** Problem record has been opened from (or associated to) the incident and you're waiting for more information from the problem management process before continuing on.
- **Awaiting Change:** Change record has been opened from (or associated to) the incident and you're waiting for more information from the change management process before continuing on.
- **Awaiting Vendor:** Waiting on information from a vendor assisting with resolution of the incident.

&nbsp;&nbsp;&nbsp;&nbsp;drawio3. Please refer the following image:

![drawio3](./images/drawio3.png)

&nbsp;&nbsp;&nbsp;&nbsp;As we can notice from the above image,drawio3.
