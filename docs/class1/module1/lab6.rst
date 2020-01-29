Importing an OpenAPI 3 specification
====================================

Next is working through an API deployment using an API specification to create a new API definition for the trading API.
Then importing the OpenAPI specification directly into controller.
Samantha's developers are able to specify all the details and endpoints and routes of the trading API in a swagger file, which they are maintaining any way as modern application developers.

1. Login
   1. Using Postman
   2. Expand the Common Tasks section
   3. Select `Login to Controller - admin`
2. Add the OpenAPI3 API definition
   1. Expand the Retail-Dev Environment
   2. Expand the Application - trading.acmefinancial.net
   3. Select `Import OAS API Definition - trading-api`
   4. Select Send to PUT the API specification
3. Link the API specification to a Gateway
   1. Within the Application - trading.acmefinancial.net section of Postman
   2. Select `Create an Application Published API - Trading-api`
   3. Note the reference to the gateway and to the apiDefinition
   4. Select Send to PUT the configuration
4. Define the path for the API and reference the API definition
   1. Within the Application - trading.acmefinancial.net section of Postman
   2. Select `Create Comp - trading - api`
   3. Note the additional publishedApiRef section
   4. Select Send to PUT the Component
   5. Change the PUT to GET to check the state of the change
