================================================
Familiarize yourself with Controller as Samantha
================================================


   
Follow these steps to complete this task:


Login to Controller as Samantha
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  1. Connect to the Jumphost from the UDF interface (all activities should be performed from the Jumphost). In UDF from the `jumphost-1` host, select `Access` and then `RDP`. 

    .. image:: ../../_static/jumphost.png
        :scale: 60 %
        :align: center

  2. Log in to the Jumphost. Enter the Jumphost credentials:

    - username: `administrator`
    - password: `BZ8D8MCVR`

  3. Open the Chrome browser

  4. Enter the URL: https://10.1.1.5

  5. Log in as Samantha using the credentials:
  
    - username: `retail-dev@acmefinancial.net`
    - password:  `Admin123!@#`

 
 
Review Samantha's view within Controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  1. Select the navigation bar in the upper left of the screen. 
   
        .. image:: ../../_static/navigation_root.png
           :scale: 60 %

  2. Select the `Services` menu. 
   
        .. image:: ../../_static/navigation_services.png
           :scale: 60 %

        - Under `Services` Samantha is restricted to three Apps supporting ACME Financial.
    
  3. Select the App named `trading.acmefinancial.net`
        
        - Note the tray that opens on the right, showing the Components that have been configured for the application.
   
  4. Explore each Component to familiarize yourself with the full application.

 
 
  +-------------------------------------------------------------------------------------+
  | Talk Track                                                                          |
  +=====================================================================================+
  | We can see at a glance the configuration state of the trading app and then go and   |
  | see the various components and pieces of the app.                                   |
  +-------------------------------------------------------------------------------------+
  


Explore the documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  +-------------------------------------------------------------------------------------+
  | Talk Track                                                                          |
  +=====================================================================================+
  | Samantha is also becoming accustomed to the new Controller API. She finds the new   |
  | UX straightforward visually, and she likes that it helps her understand the object  |
  | structure. Not to mention how it helps her learn how to use the APIs: she can see   |
  | the API call being built, the endpoint and how the JSON is structured.              |
  +-------------------------------------------------------------------------------------+


  1. From the Controller UI, select the help icon in the Navigation bar.  
    
        .. image:: ../../_static/navigation_help.png
           :scale: 60 %

        A new tab opens presenting the in-box documentation

  2. Select `API Reference` drop down
  3. Select the current version of the API Reference 
    
        .. image:: ../../_static/documentation_api.png
           :scale: 60 %


  +-------------------------------------------------------------------------------------+
  | Talk Track                                                                          |
  +=====================================================================================+
  | Samantha now has a full API reference of the Controller endpoints. She can use this |
  | to automate creating and deploying new servies.                                     |
  | The two main endpoints we'll be working with a `gateway` and `component`.           |
  +-------------------------------------------------------------------------------------+


  4. In the left side of the API Reference select the `gateways` section and explore the object.
  5. In the left side of the API Reference select the `components` section and explore the object.

In both cases note the object-based path to interact with these objects.  For example: a *Component* is an object that is a child to an *App* which is a child to an *Environment*.
`https://10.1.1.5/api/v1/services/environments/{environmentName}/apps/{appName}/components`

| Take a moment to review the Information Architecture controller employs to make sure this makes sense to you:

      .. image:: ../../_static/ia.png



 
 
 
Explore API actions in the GUI while editing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  1. From the Controller GUI web browser tab
  2. Select the `trading.acmefinancial.net` App
  3. Select Edit 
    
    .. image:: ../../_static/app_edit.png
       :scale: 60 %

  4. at the bottom of the edit screen select `VIEW API REQUEST` to review the API used to create or modify this App object.  
    
    .. image:: ../../_static/view_api_request.png
       :scale: 60 %

  5. Note the API call, the JSON body, and the copy to clipboard icon all added to enable quick and easy GUI discovery and translation to automation.

   .. image:: ../../_static/view_api_req.png

