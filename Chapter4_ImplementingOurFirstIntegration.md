## Chapter 4 (Draft)

# Implementing Our First Integration

## A clear picture

&nbsp;&nbsp;&nbsp;&nbsp;Till this point, we have seen what Inbound integration is in the context of ServiceNow, got familier with REST API explorer and got a faded picture of what we will be implementing in our first integration. I feel this is a perfect time to make that picture more clearer. Please refer the following image:

![drawio1](./images/drawio1.png)

&nbsp;&nbsp;&nbsp;&nbsp;The above image specifies that whenever an incident is created on Vendor (Company A) instance with a specific Service and assigned to Specific group (both of them should be predefined by business), The copy of incident is created on Customer (Company B) instance and assigned to specific assignment group (also predefined by business).
