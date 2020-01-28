# NGINX Controller 3.x Lab Guide

=================================

ACME Financial was founded in 1965.
During the 1980 recession in America, ACME financial spun off to provide lending assistance for its customers. This created a lending business unit and in 2001 asked me financial increased to start focusing on the retail personal finance space.
In 2020 that retail space started to define a new trading platform.
In this exercise we will begin working within that space of two business units, the lending business unit and the retail space.
Within the team that we work with to engage with Controller was David a network engineer responsible for the overall NGINX Controller platform.
Responsible for some of the security and network routing core routing requirements within the DevOps space in the lending business unit.
Olivia, a DevOps engineer, responsible for curating the pipelines and the NGINX configuration. No more app centric delivery fashion within the
within that space as well is Tony an app developer responsible for some of the core service center applications.
In the other part of the organization in the retail business unit. 
We have Samantha who's been responsible for the DevOps engineering around building pipeline and getting the new trading and other apps available to that market space.

## Familiarize yourself with Controller as Samantha

Follow these steps to complete this task:

1. Login to Controller as Samantha
   1. Open the Controller web interface and logon using the username: retail-dev@ACMEfinancial.net with the password:  Admin123!@#
2. Review Samantha's view within Controller
   1. Select the navigation bar in the upper left of the screen. ![navigation_root](_static/navigation_root.png)
   2. Select the Services menu. ![navigation_services](_static/navigation_services.png)
      1. Under Services Samantha is restricted to three Apps supporting ACME Financial.
   3. Select the App named trading.acmefinancial.net
      1. Note the tray that opens on the right, showing the Components that have been configured for the application.
   4. Explore each Component to familiarize yourself with the full application.

    We can see at a glance the configuration state of the trading application and then go in and see what makes this application tick. What are the various components and pieces.

3. Explore the documentation

    Samantha is also becoming accustomed to the new API for controller. She is going to be able to use this new UX experience to both work visually with the product as well as seeing how to automate and use the new API that's available with Controller.

    1. From the Controller UI, select the help icon in the Navigation bar.  ![navigation_help](_static/navigation_help.png)

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

## Extending the Trading application through exposing referral and upload capabilities

### Using the GUI

Samantha is responsible for the trading application has found that it's been extremely successful and adopted by the retail customers are looking to move fast.
App teams are running a rolling out new parts of the application using modern application development processes. So what we're going to see is the deployment of new financial transfer functions.
A referral program as well as some upload capabilities within the, within the controller space. So let's go ahead and begin these changes.

1. Explore the trading application
   1. Using Google Chrome, open a new tab
   2. Enter 'https://trading.dev.acmefinancial.net` as the URL
   3. Select Login
   4. enter the username: admin with the password iloveblue
   5. Note the dashboard, as we enable new features the dashboard will change, displaying these new capabilities.

2. Define a new Transfers Component of the trading.acmefinancial.net application
   1. In the Controller GUI return to the Apps section
   2. Select the App trading.acmefinancial.net
   3. Select the View icon ![view](_static/view.png) to see the full list of Components for the App
   4. Select Create Component ![create_component](_static/create_component.png)
   5. enter the name: trading-transfers
   6. enter the display name: Trading Transfers Component
   7. Select Next
   8. Select the Gateway: trading.acmefinancial.net
   9. Select Next
   10. Enter the URI: /api
   11. Select Next (skipping Methods, and Advanced sections)
   12. Add a workload group
   13. Workload Group Name: app2-servers
   14. Add Backend Workload URI: http://10.1.20.21:9804
   15. Select Publish to create the transfers capability. ![publish](_static/publish.png)
   16. Observe the Status of the Component change from Configuring to Configured to indicate it is live.

    A dev ops team or in this ACME financial organization David's responsible for the network and certificate management within the financial organization. David's team established the trading gateway for Samantha to support this new component.

    As you can see the UI space is really flexible and powerful for various scenarios or use cases within Controller, whether it's basic URI routing,  SNI routing, or a combination. This example was very basic URI routing.
    The objective of this component is to route to the servers on which the particular component code runs, this is the workload group.  A workload group is the collection of servers or upstreams.

    Controller is responsible for getting the desired configuration that we specified thorugh the GUI or the API and getting it to the actual NGINX instance to process traffic.

3. review the new section of the Trading application
   1. Return to the trading application browser tab and refresh the page
   2. Note the new capability that has been added to the right hand side of the applicaton.

Very quickly, you were able to establish a new traffic path configuration and didn't have to directly configure an NGINX instance or understand nginx.conf syntax. Through monitoring and analytics you can see this new component capable of adding value to the business and business unit.

### Using the API

Now, this is great. Samantha explored Contorller and discovered what she can do the GUI.  But most likely she is going to move forwarding to plumbing these steps and configurations into her pipeline.  We are now going to open a pipeline tool that Olivia might use and extend the trading application using the API.

1. Login as Samantha using the API
   1. From the desktop open Postman
   2. the Collection `NGINX Controller 3.0 UDF Demo & Lab` should already be loaded
   3. Open the Common Tasks section and select `Login to Controller - retail dev`
   4. Select Send

    You are now logged into the API as Samantha.  Controller returned a cookie that will be used for authenticating then executing the following commands.

2. Enable the Referrals capability
   1. In Postman open the section `Retail-Dev Environment`
   2. open the `Application - trading.acmefinancial.com` section
   3. Select `Create Comp - trading - referrals`
   4. In the right hand frame of Postman, select the Body tab
   5. Review the JSON
   6. PUT the configuration by selecting Send
   7. Change the command to GET and Send
   8. View the status of the configuration being applied in the currentStatus section and that the selfConfigState is in configuring
   9. Repeat the GET until configured equals 1

    Controller follows an API first methodology which means that the GUI is using the same APIs as you are.
    In this configuration PUT body you can see the desiredState of ingress (the incomming URI) and backend (the workloadGroups and servers).
    Through the GET you can see the eventually consistent behavior of the system as the configuration is then built and applied to the referenced NGINX instances.

3. review the new section of the Trading application
   1. Return to the trading application browser tab and refresh the page
   2. Note the new ![referrals](_static/referrals.png) capability that has been added to the applicaton.  Previously there was a ![coming_soon](_static/coming_soon.png) placeholder.

## Analytics of your application

In the previous scenario, we should we saw the expansion of the trading application. Now, let's take a look at what statistics are available within NGINX Controller for this application.

1. Viewing analytics in the GUI
   1. Using the Controller GUI tab of the web browser
   2. Using the navigation bar select the Analytics menu
   3. Select the retail-dev Dashboard
   4. Note the traffic that you created during the previous steps

    Currently, Controller 3.0 we have the ability to see all the stats available to Samantha via a dashboard. You can edit and add additional statistics, you can see some of the traffic you have been generating while through the lab.
    This will be expanded into App centricity in later releases.

2. Viewing metrics with the API
   1. Using Postman
   2. Open the Analytics section
   3. Select `get metrics with filter`
   4. Review the query settings of resolution of 30 minutes for the aggregation of SUM of 500 errors with a filter to NGINX instance 4 or 6
   5. Select Send

    The return is time series data that are a summary of status 500 messages counted every 30 minutes.  The API offers flexibility to craft a number of different queries using filters, resolution over time periods, and aggreagations.

## Adding a gateway for the mobile trading application

The trading application has been a great product with a web broswer GUI. The business unit wants to expand this to a new mobile application so that ACME Financial retail customers can do trades on the go.
To enable this noe mobile API for customers ACME Financial needs to expose a brand new gateway to the public Internet for Samantha's mobile application to receive API calls.
Within ACME Financial the request workflow requires David to get involved when any new endpoint is exposed to the public internet and to ensure security for API calls coming into the bank.
Samantha will partner with David to ask for a new gateway with a new certificate to make sure that trading API interaction is secure.
Let's work through the process of David establishing a new gateway for Samantha.

### Reviewing Role Based Access Control

1. Log out as Samantha
   1. In the Controller GUI tab of the web browser
   2. Select the retail dev user in the top right corner then
   3. Select logout
2. Log in as David
   1. Login as David using the username: admin@acmefinancial.net with the passord Admin123!@#
3. Review Role Based Access Control
   1. Review what David can access across Apps, Components, Environments
   2. Note that he can view all Environments, including Samantha's retail-dev and Olivia's lending-prod
   3. Select Platform from the navigation bar
   4. Select Roles
   5. Explore the Roles (viewing various ones) to note how a Role grants or restricts access using the API endpoints and objects.
   6. Select Users
   7. Explore what users are associated with what Roles

    As you saw, Controller can limit access to various users, such as Samantha so that she's able to self-service within her environment's and configure and specific data path instances.
    This keeps peace of mind for David that no business units collide within configuration of shared or dedicated NGINX instances and align with that many business unit needs and resource allocations.

### Adding a new Gateway

1. Add a Gateway using the GUI
   1. In the Controller GUI tab of the web browser
   2. Select the Services menu from the navigation bar
   3. Select Gateways
   4. Select Overview
   5. Select ![create](_static/create.png)
   6. Enter the Name: trading-api.acmefinancial.net
   7. Select the environment:  Retail Dev
   8. Select Next
   9. Select the Instance Reference: dev-nginx-1
   10. Select Next
   11. Add the URI: https://trading-api.acmefinancial.net
   12. Select Done
   13. For the Certificate Reference select ![Create New](_static/create_new.png)
   14. Name the new certificate: trading-api.acmefinancial.net
   15. Browse to the trading-api.dev.acmefinancial.net.crt certificate
   16. Browse to the trading-api.dev.acmefinancial.net.key key
   17. Select Submit to create the new certificate
   18. Select Next
   19. Select Next
   20. Select Publish
   21. Note that the Gateway progresses from a state of configuring to configured.

    Certificates (PEM or PKCS12) can be imported into Controller at the time they are added to a Gateway or Component, they can be defined and managed seperately (such as by a unique certificate team) and only referenced, or a file path local to the NGINX instance can be defined.  All giving unique flexibility to David and Samantha in best meeting how they want to manage their certificates.

### Importing an OpenAPI 3 specification

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

### Defining JWT token authentication with the API

Defining the secure part of the API with different workload group servers and authentication with a JWT token. This ensures that API calls have a security policy that's using an identity provider.
In this case the token is a barrier type token to make sure that no one can just randomly trade stocks without knowing some secret to access the API.

1. Create a new identity provider
   1. Within the Application - trading.acmefinancial.net section of Postman
   2. Select `Create an Identity Provider - trading JWT Inline Keys`
   3. Note the reference to the Environment
   4. Select Send to PUT the configuration
2. Define the component to use JWT authentication
   1. Within the Application - trading.acmefinancial.net section of Postman
   2. Select `Create comp - trading - api-secure`
   3. Note the ingress URIs and security sections of the JSON
   4. Select Send to PUT the configuration
   5. Change the call to GET to check the status of the configuration being applied
3. Test the mobile API without using authentication
   1. Using Postman
   2. Expand the temp section
   3. Select `testing jwt`
   4. Select the ![Auth tab](_static/auth_tab.png) in the Postman window
   5. Change the type to ![No Auth](_static/no_auth.png)
   6. Select Send
   7. Note that 401 Authorization Required is returned
4. Test the mobile API with a JWT Token
   1. Continuing from the steps above
   2. Select the ![Auth tab](_static/auth_tab.png) in the Postman window
   3. Change the type to ![Bearer Token](_static/bearer_token.png)
   4. The token should be present - if not use: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJPbmxpbmUgSldUIEJ1aWxkZXIiLCJpYXQiOjE1NzMxNDQxMjksImV4cCI6MTYwNDY4MDEyOSwiYXVkIjoiRm91YWQiLCJzdWIiOiJCb2JUaGVTcG9uZ2UiLCJSb2xlIjoidXNlciJ9.ykcdfE6B993gBDxcsLzIJVp6XTqaTSywr6HuUNfyimw
   5. Select Send
   6. Note that the API call suceeds
5. View the trasaction in the Trading GUI
   1. Return to the browser tab with the trading API
   2. Refresh the display
   3. Note the list of Last Transactions for a new one from today

### Reviewing configuration state through the API at a higher level

Just like everything else we can go and do a get and see if we're in a fully configured state. And we can see that state from a higher level order. So we can actually take a look at the configuration state across an Application or Environment.
Within the retail-dev environment. So we want to see a list of all of our components and gateways and what children we have within the space, how many components, How many apps, etc.

1. Return the objects within an Environment
   1. Using Postman
   2. Open the Retail-Dev Environment
   3. Open Application - trading.acmefinancial.net
   4. Select `Create Env - retail-dev`
   5. Change the PUT to a GET
   6. Note the URL, it refers to the retail-dev Environment object
   7. Select Send to GET the object
   8. Note the applications, certificates, and gateways in their resprctive reference sections
   9. In the state section note the `childrenConfigState` that refers to any of the child objects and their status
   10. Note the `selfConfigState` which refers to the Environment itself

## Extending www.acmefinancial.net with a blog Component

Samantha is looking to expand on the marketing sites that are promoting the various technologies that the ACME Financial organization has been able to produce.
She wants to build a brand new application component within the marketing page www.acnefinancial.net and introduce the new blog capability so they can start blogging about the trading application.
So let's return to Controller as Samantha and take a look at some of the additional feature functionality with the ADC use cases of URI rewrite.

1. Log out as David
   1. Returing to the Controller GUI
   2. Select ![admin istrator](_static/admin_istrator.png) in the top right
   3. Select ![Log Out](_static/log_out.png)
2. Log in as Samantha
   1. Login as Samantha using the username: retain-dev@acmefinancial.net with the passord Admin123!@#
3. Review the Components added via the API
   1. Select Services from the navigation menu
   2. Select Apps
   3. Select trading.acmefinancial.net
   4. Review the componnets added through the API, note the commonality between the API and GUI
4. Add blog page to the main ACME Financial site with a URI rewrite
   1. Return to the list of all Apps
   2. Select www.acmefinancial.net
   3. Select View
   4. Select Create Component
   5. Name: blog
   6. Gateway: www.acmefinancial.net
   7. URI: /blog
   8. Add Workload Group: wordpress
   9. Add Backend Workload URIs:
      1. http://10.1.20.21:8003
      2. http://10.1.20.22:8003
   10. Add URI Rewrite:
       1. incoming pattern: ^/blog/(.*)$
       2. rewrite pattern: /blog/wordpress/wwwsite/$1?
   11. Publish
5. Test the URI rewrite
    1. In a new tab in the web browser enter: http://www.dev.acmefinancial.net/blog/biganouncement
    2. In the returned web page note that the path is being rewritten to: /blog/wordpress/wwwsite/biganouncement

## The www.acmefinancial.net is having issues

Let's at the merchandise site that's ACME Financial retail has. They have embraced this whole ACME corporate branding and new hipsters that love these kinds of chochky branded materials.  ACME Financial decided to put up a merchandise site.
But support has been receiving some complaints. In end to end testing of the ACME store in the development environment it was identified that the shopping cart experience is not ideal.
Let's take a look at what's happening there. Starting off with a little debugging session.

1. View the symptom
   1. Open a tab in the web browser
   2. Go to the site: https://merch.dev.acmefinancial.net
   3. Browse the site and add something to your shopping cart
   4. Open the Shopping Cart
   5. Refresh the shopping cart a few times and notice that the cart empties
      1. The cart state is tracked in a cookie and the cookie is not shared across the backend servers
2. View the JSON of the Component
   1. Using Postman
   2. Expand `Retail-Dev Environment`
   3. Expand `Application - merch.acmefinancial.net`
   4. Select `Create Component - shop - no persist`
   5. Review the JSON body
      1. this is the existing configuration from Samantha's pipeline
      2. Note that no persistence is defined to aide in loadbalancing across workloads
3. Verify new developer cookie persistence settings
   1. Select `Create Component - shop`
   2. Review the JSON body
   3. Note the `sessionPersistence` section
   4. Select Send to PUT the new configuration
   5. Change the method to GET to check for the configuration to be applied
4. View the solution
   1. Return to the browser tab with https://merch.dev.acmefinancial.net
   2. Browse the site and add something to your shopping cart
   3. Open the Shopping Cart
   4. Refresh the shopping cart a few times and notice that the cart does not empty any longer

## Triaging and handling 500 errors with a large call center application

Let's take a look at some of the problems with a large call center application that Olivia is responsible for. 
It's a complicated three tier application with internal services that are communicating between each other.
Olivia is getting some reports from the call center agents at the service center application is having issues.  We are going to troubleshoot and understand what might be going on.
It looks like some of the issues might be with the ticket processing service, but let's take a look at what the Controller dashboards could show us about the application and components.

1. Log out as Samantha
   1. Returing to the Controller GUI
   2. Select retail dev in the top right
   3. Select ![Log Out](_static/log_out.png)
2. Log in as Olivia
   1. Login as Olivia using the username: lending-admin@acmefinancial.net with the passord Admin123!@#
3. Test the web site
   1. Using Postman
   2. Expand the Traffic Tests section
   3. Select the ticketprocessing.internal.acmefinancial.net request
   4. Select Send a few times
   5. Note that you will randomly receive a 500 response
4. Review statsus codes
   1. Open Analytics from the Navigation bar
   2. Select the Lending-Prod dashboard
   3. Scroll to the bottom and you will find the internal system - 500 service errors graph
   4. Note the spikes of 500 errors
5. Identify where the 500 error is coming from
   1. Returning to Postman
   2. select send until you receive a 500 error
   3. Note the serverPort in the response
      the 500 error only happens when the request is routed to a specific workload serverPort
6. Triage a workaround
   1. Return to the Controller GUI
   2. Select Service from the Navigation bar
   3. Select the App servicecenter.acmefinancial.net
   4. Select the Component ticketprocessing.internal.acmefinancial.net
   5. Select ![Edit Component](_static/edit_component.png)
   6. Select Workload Groups
   7. Edit the servers workload group
   8. Edit the two backend workload URIs using port 6203
      1. Set Is Down to True
      2. Select Done
   9. Publish the changes
7. Test the web site again
   1. Using Postman
   2. Expand the Traffic Tests section
   3. Select the ticketprocessing.internal.acmefinancial.net call
   4. Select Send a few times
   5. Note that you no longer reseive a 500 response
8. Setting a Health monitor from the pipeline
   1. Using Postman
   2. Expand `Application - servicecenter.acmefinancial.net`
   3. Expand `Establish APIM Defs and Components - ticketprocessing.internal.acmefinancial.net`
   4. Select `Create Component - mon - ticketprocessing.internal.acmefinancial.net`
   5. Note the monitoring section
   6. Note that isDown is back to false for each workload URI
   7. Select Send to PUT this configuration
9. Test the web site again
   1. Using Postman
   2. Expand the Traffic Tests section
   3. Select the ticketprocessing.internal.acmefinancial.net call
   4. Select Send a few times
   5. Note that you no longer reseive a 500 response

A better configuration.  Servers are no longer tagged as down permanently in the configuration. The system is tagging the servers as down.
Adding monitoring to this configuration so that instead of just having to manually up down things we can let NGINX be responsible for health checking
actively or passively based on the configuration of monitoring ensuring health and availability of the service.

## Protecting your application with rate limiting

There are reports to the mortgage team that some folks have had the inability to login.
The mortgage team has reported: "hey, our service is seeing some massive spike and CPU load."
So let's provide some relief to the mortgage team and take a look at the configuration of the mortgage application again we can see

The mortgage application in our pipeline has a couple different components, a web login and web API endpoints and we see the configuration right now via get

1. GET the configuration
   1. Using Postman
   2. Expand the Lending-Prod Environment section
   3. Expand Application - mortgage.acmefinancial.net
   4. Select Create Component - login
   5. Note the URI and that the service is fully encrypted to the workloads
2. Review rate limiting
   1. Select Create Component -login - with rate 
   2. Note the Security section and the rateLimit
      The rate limit is set low ( 1 second ) to provide some relief.
   3. Select Send to PUT the configuration change
3. Test the Rate Limit configuration
   1. Open a tab in the web browser
   2. enter the URL: https://mortgage.acmefinancial.net/login
   3. Refresh the page quickly a few times
   4. Note the 429 that is returned if you refresh the page too quickly

