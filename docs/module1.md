## Familiarize yourself with Controller as Samantha

Follow these steps to complete this task:

1. Login to Controller as Samantha
   1. Open the Controller web interface and logon using the username: retail-dev@ACMEfinancial.net with the password:  Admin123!@#
2. Review Samantha's view within Controller
   1. Select the navigation bar in the upper left of the screen. ![navigation root](_static/navigation_root.png)
   2. Select the Services menu. ![services](_static/navigation_services.png)
      1. Under Services Samantha is restricted to three Apps supporting ACME Financial.
   3. Select the App named trading.acmefinancial.net
      1. Note the tray that opens on the right, showing the Components that have been configured for the application.
   4. Explore each Component to familiarize yourself with the full application.

    We can see at a glance the configuration state of the trading application and then go in and see what makes this application tick. What are the various components and pieces.

3. Explore the documentation

    Samantha is also becoming accustomed to the new API for controller. She is going to be able to use this new UX experience to both work visually with the product as well as seeing how to automate and use the new API that's available with Controller.

    1. From the Controller UI, select the help icon in the Navigation bar.  ![help](_static/navigation_help.png)

        A new tab opens presenting the in-box documentation

    2. Select API Reference drop down
    3. Select the current version of the API Reference ![documentation_api](_static/documentation_api.png)

        Samantha now has a full API reference of how to use the various endpoints that are available and can walk through the various endpoints to be able to automate from login to creating and deploying new services.
        The two main endpoints that we will be working with are gateway and component

    4. In the left side of the API Reference select the gateways section and review the options.
    5. In the left side of the API Reference select the components section and review the options.

        In both cases note the object based path to interact with these objects.  For example: a Component is an object that is a child to an App which is a child to an environment.
        `https://10.1.1.5/api/v1/services/environments/{environmentName}/apps/{appName}/components`

4. Explore API actions in the GUI while editing

    1. From the Controller GUI web browser tab
    2. Select the trading.acmefinancial.net App
    3. Select Edit ![edit](_static/edit.png)
    4. at the bottom of the edit screen select VIEW API REQUEST to review the API used to create or modify this App object.  ![view_api_request](_static/view_api_request.png)
    5. Note the API call, the JSON body, and the copy to clipboard icon all added to enable quick and easy GUI discovery and translation to automation.
