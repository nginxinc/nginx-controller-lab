==============================================================================
Extend the Trading app: add referral and upload
==============================================================================

A: Using the GUI
================

+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Samantha owns the trading app: it's been extremely successful and rapidly adopted by retail |
| customers. Dev teams are rolling out new parts of the app using modern app processes like   |
| automated testing and CI/CD. We're going to deploy some new features for the app:           |
|                                                                                             |
|  - the ability to transfer funds,                                                           |
|  - a referrals program, and                                                                 |
|  - file uploads                                                                             |
+---------------------------------------------------------------------------------------------+

Explore the trading application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Using Google Chrome on the Jumpbox, open a new tab
    2. Enter `https://trading.dev.acmefinancial.net` as the URL
    3. Select `Login`
    4. enter the credentials:

      - username: `matt`
      - password: `ilovef5`
      
    5. Note the dashboard. As we enable new features the dashboard will change, displaying these new capabilities.

|trading_transfer_before|


Define a new Transfers Component of the trading.acmefinancial.net application (Withing the retail-dev environment)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. In the Controller GUI return to the `Apps` section
    2. Select the App `trading.acmefinancial.net`
    3. Select the `View` icon |icon| to see the full list of Components for the App
    
    .. |icon| image:: ../../_static/view.png

    4. Select `Create Component` 
    
    .. image:: ../../_static/create_component.png

    5. enter the name: `trading-transfers`
    6. enter the display name: `Trading Transfers Component`
    7. Select Next
    8. Select the Gateway: `trading.acmefinancial.net`
    9. Select Next
    10. Click the `Add URI` link on the upper right. Enter the URI: `/api`
    11. Select Next (skipping `Methods`, and `Advanced sections`)
    12. Click the `Add Workload Group` link in the upper right and enter a new group name: `app2-servers`
    13. Add Backend Workload URI: `http://10.1.20.21:9804`. Click `Done`.
    14. Select `Publish` to create the transfers capability.     
    
    .. image:: ../../_static/publish.png
    
    15. Observe the Status of the Component change from `Configuring` to `Configured` to indicate it is live.     
    
    .. image:: ../../_static/configuring.png
    

+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| David’s team established the trading gateway for Samantha to support this new component.    |
| The Controller UI is both flexible and powerful, whether trying to understand what an app's |
| components are or doing app-based URI or SNI routing, or a combination.                     |
| What we're doing here is routing to the servers running the code: the `workload` group. A   |
| Workload Group is a section of servers or upstreams. Controller is responsible for applying |
| the configuration entered through the GUI or API, and realizing it at the actual NGINX      |
| instance to process traffic.                                                                |
+---------------------------------------------------------------------------------------------+

Review the new section of the Trading application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Return to the trading application browser tab and refresh the page
    2. Note the new capability that has been added to the right hand side of the application.

|trading_transfer_after|


+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| You were able to establish a new traffic path configuration and didn't have to directly     |
| configure an NGINX instance or understand nginx.conf. Through Controller's monitoring and   |
| analytics you can see this new component, ready and able to add value to the business unit  |
| and to their customers.                                                                     |
+---------------------------------------------------------------------------------------------+

B: Using the API
================

+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Samantha explored Controller and discovered what she can do in the GUI. But she's most      |
| likely going to go forwards by adding these steps and configurations into her pipeline.     |
| We're now going to open a tool that Olivia might use to extend the trading app via the API. |
+---------------------------------------------------------------------------------------------+


Login as Samantha using the API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. From the desktop open Postman
    2. the Collection `NGINX Controller 3.0 UDF Demo & Lab` should already be loaded
    3. Open the `Common Tasks` section 
    
 |open|
 
    4. Select `Login to Controller - retail dev`
 
 |login|
    
    5. Select `Send`

      You are now logged into the API as Samantha.  Controller returned a cookie that will be used for authenticating then executing the following commands.


Enable the Referrals capability
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. In Postman open the section `Retail-Dev Environment` 
    2. open the `Application - trading.acmefinancial.com` section
    3. Select `Create Comp - trading - referrals`

     |trading|

    4. In the right hand frame of Postman, select the `Body` tab

     |body|

    5. Review the JSON
    6. Make sure that the method is set to "PUT"

     |method|
      
    7. Click `Send`
    8. Change the method to "GET" and click `Send` again
    
    
    9. View the status of the configuration being applied in the `currentStatus` section and that the `selfConfigState` is in "configuring"
    10. Repeat the GET until "configured" equals "1"
    
      |configured|
      
+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Controller follows an *API-First* methodology, which means that what you see in the GUI is  |
| using the very same APIs Controller provides.                                               |
| In the pervious PUT request's body you can see the desiredState for ingress (the incoming   |
| URI) and backend (the workload groups and servers). Through the GET request you can see the |
| *eventually consistent* behavior of the system as the config is built and then applied to   |
| the specified NGINX instance.                                                               |
+---------------------------------------------------------------------------------------------+
 

Review the new section of the Trading application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Return to the trading application browser tab and *refresh the page* (from the Jumphost)
    2. Note the new capability that has been added to the application: |referrals| 
    3. Previously there was a placeholder: |coming_soon|

.. |trading_transfer_before| image:: ../../_static/trading_transfer_before.png
    
.. |trading_transfer_after| image:: ../../_static/trading_transfer_after.png
    
.. |coming_soon| image:: ../../_static/coming_soon.png
    :scale: 30 %

.. |referrals| image:: ../../_static/referrals.png
    :scale: 30 %
    
.. |open| image:: ../../_static/postman_commontasks.png

.. |login| image:: ../../_static/postman_login.png
 
.. |trading| image:: ../../_static/postman_showtree.png
 
.. |body| image:: ../../_static/postman_body.png
 
.. |configured| image:: ../../_static/postman_configuredjson.png

.. |method| image:: ../../_static/postman_changemethod.png
