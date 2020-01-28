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
