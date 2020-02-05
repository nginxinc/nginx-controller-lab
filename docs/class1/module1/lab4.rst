==========================================
Reviewing Role Based Access Control (RBAC)
==========================================

Log out as Samantha
^^^^^^^^^^^^^^^^^^^^^^

    1. Select the Controller GUI tab in Chrome
    2. Select the `retail dev` user in the top right corner
    3. Select logout

Log in as David
^^^^^^^^^^^^^^^^^^

    1. Login as David using the credentials: 
    
      - username: `admin@acmefinancial.net`
      - password: `Admin123!@#`

Review Role Based Access Control (RBAC)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Review what David can access across `Apps`, `Components`, `Environments` (in the `Services` Menu)
    2. Note that he can view all `Environments`, including Samantha's `retail-dev` and Olivia's `lending-prod`
    3. Select `Platform` from the navigation bar
    4. Select `Roles`
    5. Explore the Roles (viewing various ones) to note how a Role grants or restricts access using the API endpoints and objects.
    6. Select `Users`
    7. Explore what users are associated with what Roles


+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| As you saw, Controller can limit users' access to various objects. For example, Samantha is |
| able to manage and make changes within her environments and configure specific data path    |
| instances, enabling self-service for the areas she owns.                                    |
| This ensures David's peace of mind that no business units configuration changes collide on  |
| shared or dedicated NGINX instances.                                                        |
+---------------------------------------------------------------------------------------------+
    
    
