====================================
Importing an OpenAPI 3 specification
====================================

Next is working through an API deployment using an API specification to create a 
new API definition for the trading API. Then importing the OpenAPI specification directly 
into controller. Samantha's developers are able to specify all the details and endpoints 
and routes of the trading API in a swagger file, which they are maintaining any way as 
modern application developers.

Login
^^^^^

   1. Go to Postman on the Jumphost 
   2. Expand the Common Tasks section
   3. Select `Login to Controller - admin` and click Send on the right hand pane

Add the OpenAPI3 API definition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   1. Expand the `Retail-Dev Environment`
   2. Expand the `Application - trading.acmefinancial.net`
   3. Select `Import OAS API Definition - trading-api`
   4. Click on Send to push the API specification (via PUT method)

Link the API specification to a Gateway
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   1. Within the `Application - trading.acmefinancial.net` section of Postman
   2. Select `Create an Application Published API - Trading-api`
   3. Note the reference to the gateway and to the apiDefinition in the body
   4. Click on Send to push this configuration (PUT method)

Define the path for the API and reference the API definition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   1. Within the `Application - trading.acmefinancial.net` section of Postman
   2. Select `Create Comp - trading - api`
   3. Note the additional publishedApiRef section
   4. Change the GET method to a PUT method (we need to create the object first)
   5. Click on Send to create this Component (via PUT method)
   6. Change the PUT method back to a GET method to check the state of the change
