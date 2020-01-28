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
