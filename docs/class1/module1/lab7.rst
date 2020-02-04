===============================================================
Understand configuration state via the API
===============================================================

Just like with everything else in Controller, we can do a GET request to see if we're in a fully 
configured state. We're able to look at config state from a high-level, such as across an App or an Environment.


For example: Within the `retail-dev` environment, we want to see:

- a list of all of our components and gateways
- what children we have within the space
- How many components? apps? 
- etc.

Return the objects within an Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Using Postman in the JumpHost
    2. Open the `Retail-Dev Environment` section
    3. Open `Application - trading.acmefinancial.net`
    4. Select `Create Env - retail-dev`
    5. Change the PUT method to a GET method
    6. Note the URL, it refers to the `retail-dev` Environment object
    7. Click `Send` to GET the object
    8. Note the `applications`, `certificates`, and `gateways` in their respective reference sections
    9. In the `state` section note the `childrenConfigState` that refers to any of the child objects and their status
    10. Note the `selfConfigState` which refers to the Environment itself
