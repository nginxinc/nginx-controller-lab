Reviewing configuration state through the API at a higher level
===============================================================

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
