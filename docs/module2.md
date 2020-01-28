## Extending the Trading application by exposing referral and upload capabilities

### Using the GUI

Samantha is responsible for the trading application has found that it's been extremely successful and adopted by the retail customers are looking to move fast.
App teams are running a rolling out new parts of the application using modern application development processes. So what we're going to see is the deployment of new financial transfer functions.
A referral program as well as some upload capabilities within the, within the controller space. So let's go ahead and begin these changes.

1. Explore the trading application
   1. Using Google Chrome, open a new tab
   2. Enter `https://trading.dev.acmefinancial.net` as the URL
   3. Select Login
   4. enter the username: `admin` with the password `iloveblue`
   5. Note the dashboard, as we enable new features the dashboard will change, displaying these new capabilities.

2. Define a new Transfers Component of the trading.acmefinancial.net application
   1. In the Controller GUI return to the Apps section
   2. Select the App `trading.acmefinancial.net`
   3. Select the View icon ![view](_static/view.png) to see the full list of Components for the App
   4. Select Create Component ![create_component](_static/create_component.png)
   5. enter the name: `trading-transfers`
   6. enter the display name: Trading Transfers Component
   7. Select Next
   8. Select the Gateway: `trading.acmefinancial.net`
   9. Select Next
   10. Enter the URI: `/api`
   11. Select Next (skipping Methods, and Advanced sections)
   12. Add a workload group
   13. Workload Group Name: `app2-servers`
   14. Add Backend Workload URI: `http://10.1.20.21:9804`
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