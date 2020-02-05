===================================================
Import an OpenAPI 3 specification (in PREVIEW)
===================================================

+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Samantha's org wants to add a new API to the trading app. Samantha's developers are able to |
| specify all the details, endpoints and routes of the API in a swagger file (they maintan    |
| this swagger file as part of being a modern app dev). We'll go through deploying this API   |
| and creating a new definition, and then we'll import the OpenAPI specification directly     |
| Controller.                                                                                 |
+---------------------------------------------------------------------------------------------+

Login
^^^^^

    1. Go to Postman on the Jumphost 
    2. Expand the `Common Tasks` section
    3. Select `Login to Controller - admin` and click `Send` on the right hand pane
    
    |login|

Add the OpenAPI3 API definition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Expand the `Retail-Dev Environment`
    2. Expand the `Application - trading.acmefinancial.net`
    3. Select `Import OAS API Definition - trading-api`
     |treeref|
    
    4. Click on `Send` to push the API specification (via PUT method)

Link the API specification to a Gateway
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Within the `Application - trading.acmefinancial.net` section of Postman
    2. Select `Create an Application Published API - Trading-api`
    3. Note the reference to the gateway and to the apiDefinition in the body
       |bodyref| 
  
    4. Click on `Send` to push this configuration (PUT method)

Define the path for the API and reference the API definition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Within the `Application - trading.acmefinancial.net` section of Postman
    2. Select `Create Comp - trading - api` 
    3. Note the additional publishedApiRef section
  
     |publishedapi|
    
    4. Click on `Send` to create this Component (via PUT method)
    5. Change the PUT method back to a GET, and then re-run the API as GET to check the state of the change
    
  .. image:: ../../_static/postman_changemethod.png
  
  .. |bodyref| image:: ../../_static/postman_apitogw_body.png
  
  .. |login| image:: ../../_static/postman_login.png
  
  .. |treeref| image:: ../../_static/postman_oassnip.png
  
  .. |publishedapi| image:: ../../_static/postman_publishedapi.png
