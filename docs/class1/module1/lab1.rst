================================================
Familiarize yourself with Controller as Samantha
================================================

Follow these steps to complete this task:

Login to Controller as Samantha
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  1. Connect to the Jumphost from the UDF interface (all activities should be performed from the Jumphost). In UDF from the `jumphost-1` host, select `Access` and then `RDP`. 

    .. image:: ../../_static/jumphost.png
        :scale: 60 %

  2. Log in to the Jumphost. Enter the Jumphost credentials:
    - username: `administrator`
    - password: `BZ8D8MCVR`

  3. Open the Chrome browser

  4. Enter the URL: https://10.1.1.5

  5. Log in as Samantha using the credentials:
    - username: `retail-dev@ACMEfinancial.net`
    - password:  `Admin123!@#`

Review Samantha's view within Controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  1. Select the navigation bar in the upper left of the screen. 
   
        .. image:: ../../_static/navigation_root.png
           :scale: 60 %

  2. Select the `Services` menu. 
   
        .. image:: ../../_static/navigation_services.png
           :scale: 60 %

        1. Under `Services` Samantha is restricted to three Apps supporting ACME Financial.
    
  3. Select the App named `trading.acmefinancial.net`
        
        1. Note the tray that opens on the right, showing the Components that have been configured for the application.
   
  4. Explore each Component to familiarize yourself with the full application.

    We can see at a glance the configuration state of the trading application and then go in and see what makes this application tick. What are the various components and pieces.

Explore the documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Samantha is also becoming accustomed to the new API for Controller. She finds the new UX experience straightforward to work both visually with the product as well as understanding the object structure and how to automate with Controller's API as she views each configuration and examines the JSON bodies and API calls at the end.

  1. From the Controller UI, select the help icon in the Navigation bar.  
    
        .. image:: ../../_static/navigation_help.png
           :scale: 60 %

        A new tab opens presenting the in-box documentation

  2. Select `API Reference` drop down
  3. Select the current version of the API Reference 
    
        .. image:: ../../_static/documentation_api.png
           :scale: 60 %

Samantha now has a full API reference of how to use the various endpoints that are available. She can use this reference to automate creating and deploying new services.
The two main endpoints that we will be working with are `gateway` and `component`.

  4. In the left side of the API Reference select the `gateways` section and explore the object.
  5. In the left side of the API Reference select the `components` section and explore the object.

In both cases note the object based path to interact with these objects.  For example: a Component is an object that is a child to an App which is a child to an environment.
`https://10.1.1.5/api/v1/services/environments/{environmentName}/apps/{appName}/components`

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

