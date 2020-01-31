===================================
Reviewing Role Based Access Control
===================================

Log out as Samantha
^^^^^^^^^^^^^^^^^^^^^^

    1. In the Controller GUI tab of the web browser
    2. Select the retail dev user in the top right corner then
    3. Select logout

Log in as David
^^^^^^^^^^^^^^^^^^

    1. Login as David using the username: admin@acmefinancial.net with the passord Admin123!@#

Review Role Based Access Control
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Review what David can access across Apps, Components, Environments (in the `Services` Menu)
    2. Note that he can view all Environments, including Samantha's retail-dev and Olivia's lending-prod
    3. Select Platform from the navigation bar
    4. Select Roles
    5. Explore the Roles (viewing various ones) to note how a Role grants or restricts access using the API endpoints and objects.
    6. Select Users
    7. Explore what users are associated with what Roles

      As you saw, Controller can limit access to various users, such as Samantha so that she's able to self-service within her environment's and configure and specific data path instances.
      This keeps peace of mind for David that no business units collide within configuration of shared or dedicated NGINX instances and align with that many business unit needs and resource allocations.
