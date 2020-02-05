==============================================
Add a blog Component to www.acmefinancial.net
==============================================


+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Samantha wants to expand on the marketing sites promoting ACME Financial technology. She    |
| wants to build a new app component for the acme financial app - a blog.                     |
| This will allow her team to start blogging about the trading app, to spark interest and     |
| connection with their customers.                                                            |
| Let's take a look at additional feature functionality in the URI rewrite use case.          |
+---------------------------------------------------------------------------------------------+


Log out as David
^^^^^^^^^^^^^^^^^^^

    1. Returning to the Controller GUI
    2. Select |admin| in the top right
    3. Select |logout|

Log in as Samantha
^^^^^^^^^^^^^^^^^^^^^

    1. Login as Samantha using the credentials:
    
      - username: `retail-dev@acmefinancial.net`
      - password: `Admin123!@#`

Review the Components added through the API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Select `Services` from the navigation menu in the Controller GUI
    2. Select `Apps`
    3. Select `trading.acmefinancial.net`
    4. Review the components added through the API, note the commonality between the API and GUI

Add the blog page to the main ACME Financial site with a URI rewrite
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Return to the list of all Apps
    2. Select `www.acmefinancial.net`
    3. Select *View*
    4. Select *Create Component*
    5. Enter the name `blog`, then click *Next*
    6. Choose the appropriate gateway to reference `www.acmefinancial.net`, then click *Next*
    7. Add the URI `/blog`, then click *Done*
    8. Add a Workload Group and name it *wordpress*
    9. Add *Backend Workload* URIs for the *Component* URI:

      1. `http://10.1.20.21:8003`
      2. `http://10.1.20.22:8003`
    
    10. Add URI Rewrite to match any URI starting with /blog/ and rewrite it to prepend /blog/wordpress/wwwsite/. Use the regex pattern specified below: the incoming pattern catches what's been specified in the URL after */blog/*, and then puts that into the `$1` variable to rewrite the URI as /blog/wordpress/wwwsite/$1.

        1. incoming pattern: **^/blog/(.*)$**
        2. rewrite pattern: **/blog/wordpress/wwwsite/$1?**
    
    11. Press *Publish*

Test the URI rewrite
^^^^^^^^^^^^^^^^^^^^^^^

    1. In a new tab in the web browser (in the Jumphost) enter: 
    `http://www.dev.acmefinancial.net/blog/biganouncement`
    
    2. In the returned web page note that the path is being rewritten to: 
    /blog/wordpress/wwwsite/biganouncement

|returnpage|

.. |admin| image:: ../../_static/admin_istrator.png
    :scale: 50 %

.. |logout| image:: ../../_static/log_out.png
    :scale: 50 %

.. |returnpage| image:: ../../_static/blog_return_page.png
    :scale: 50 %
