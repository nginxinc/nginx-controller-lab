The www.acmefinancial.net is having issues
==========================================

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
