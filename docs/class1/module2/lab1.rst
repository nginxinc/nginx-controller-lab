==========================================
 www.acmefinancial.net is having issues
==========================================

+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Let's check out the merchandise site for ACME Financial retail.                             |
| Customers have embraced the ACME corporate branding, with hipsters especially loving these  |
| kinds of ACME-branded materials. In support of this - and seeing an opportunity to expand   |
| revenue, ACME Financial has decided to put up a merchandise site.                           |
| However, ACME customer support has been receving complaints about the store experience.     |
| In their dev pipeline they discovered during the end-to-end testing phase of the workflow   |
| that the shopping cart experience isn't ideal.                                              |
| Let's take a look at what's happening there and see if we can figure out what's going on.   |
+---------------------------------------------------------------------------------------------+


View the symptoms
^^^^^^^^^^^^^^^^^

    1. Open a tab in Chrome (in the Jumphost)
    2. Go to the site: `https://merch.dev.acmefinancial.net`
    3. Browse the site and add something to your shopping cart
    4. Open the Shopping Cart
    5. Refresh the shopping cart a few times and notice that the cart empties

      - The shopping cart items are mapped to the users' session state, however the session state is not shared between the backend servers.

View the JSON of the create component request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Using Postman (in the Jumphost)
    2. Expand `Retail-Dev Environment`
    3. Expand `Application - merch.acmefinancial.net`
    4. Select `Create Component - shop - no persist`
    5. Review the JSON body in this request
    
    |nopersist|

      - this is the existing configuration from Samantha's pipeline
      - Note that no persistence is defined to help in loadbalancing across workloads

    6. Change the method to GET and click send to verify the configure state doesn't currently have persistence enabled



Verify new developer cookie persistence settings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Change the config to enable session persistence, and sharing of the session state between the workloads

    1. Select `Create Component - shop`
    2. Review the JSON body
    3. Note the `sessionPersistence` section
    
    |persist|
    
    4. Click on `Send` to update the configuration (PUT method)
    5. Change the method to GET to check for the configuration to be applied

View the solution
^^^^^^^^^^^^^^^^^

    1. Return to the browser tab with `https://merch.dev.acmefinancial.net`
    2. Browse the site and add something to your shopping cart
    3. Open the Shopping Cart
    4. Refresh the shopping cart a few times and notice that the cart does not empty any longer


  .. |persist| image:: ../../_static/postman_cookiepersist.png
  
  .. |nopersist| image:: ../../_static/postman_cookienopersist.png
