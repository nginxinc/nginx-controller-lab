Lab 2 - Application Security (API)
##################################

The goal of this lab is to configure the Controller Application Security module through the API.

.. IMPORTANT::
    Estimated completion time: 5 minutes

.. NOTE::
    Lab instructions are written as if the student is executing the steps
    from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.


Alter Security Settings in API
------------------------------

Do you know you could have enabled WAF and managed its settings using the Controller's REST API?
This can be accomplished by using a tool such as Postman or via an automated configuration management tool such as Red Hat Ansible.
In this lab, we will be using the Postman application on the Windows jumphost.


Update a Component's Security Settings using Postman
----------------------------------------------------

#. On the jumphost, open **Postman**. Expand the **NGINX Controller 3.x** Collection.

   .. image:: ../media/PMcoll.png
      :width: 400

#. Expand **Common Tasks**, **User Logon**, and select the **Login to Controller
   – Natasha Romanoff - AD** request.

   .. image:: ../media/PMcoll2.png
      :width: 400

#. In Postman select **Send**.

   .. image:: ../media/PMsend1.png
      :width: 600

   .. NOTE::
      Controller responds with a "204 No Content" response and an authentication cookie. 

#. Expand the **Retail-Development Environment**, **Application - trading** folder. 
   Open the **Application trading** subfolder and select the request name **2) Create Component - main (CAS monitoring)**.

   .. image:: ./media/PMTradingMainCASMonitoring.png
      :width: 400

#. Click the **Body** view in the Postman request area. Look over the PUT request payload. 
   The JSON properties under ``desiredState``, ``security`` 
   should look familiar based on the Component you deployed in the previous lab.

   .. image:: ./media/PMTradingMainCASMonitoringBody.png

#. In Postman select **Send**.

   .. image:: ./media/PMTradingMainCASMonitoringSend.png
      :width: 800

   .. NOTE::
      Controller follows an "eventual consistency model". The API responded to the Postman request with a "202 Accepted" status code.
      If you were to look back at the Controller UI, you would notice it is now working to bring about the desired state. 

   .. image:: ./media/PMTradingMainCASMonitoringConfiguring.png
      :width: 600

Verify Component Changes
------------------------

#. Open Chrome Browser. If the Controller tab is not already open from the previous lab, perform the following login steps.

#. Access the NGINX Controller UI through the provided bookmark.

   .. image:: ../media/ControllerBookmark.png
      :width: 600

#. Login with the ``Natasha Romanoff`` account who is an (unprivileged) NGINX Controller user.

+---------------------------+-------------------+
|      Username             |    Password       |
+===========================+===================+
| natasha@acmefinancial.net | ``Natasha123!@#`` |
+---------------------------+-------------------+

   .. image:: ../media/ControllerLogin-Natasha.png
        :width: 400

#. Navigate to the **Services** menu.

    .. image:: ../media/Tile-Services.png
        :width: 200

#. Select the **Apps** tile.

   .. image:: ../media/Services-Apps.png
      :width: 200

#. Open the **Trading Application (CAS)** app. Note that the **Trading Main** component's **WAF Enablement Status** is "On", and the **WAF Monitoring Only Status** is "On".

    .. image:: ./media/PMTradingMainCASMonitoringVerifyApp.png

#. Click the **Components** section. 

    .. image:: ./media/PMTradingMainCASMonitoringVerifyComponent.png


Congratulations! You have successfully completed the |classbold| lab. You may close your connection to the jumphost.
--------------------------------------------------------------------------------------------------------------------
