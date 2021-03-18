Lab 2 - Programmatic ADC App Creation
################################################

The goal of this lab is for the student to deploy an app component using the NGINX Controller API.
This lab uses Postman as a proxy for programmatic deployments customers might perform through automation tools or a CI/CD pipeline.

.. IMPORTANT::
    Estimated completion time: 5 minutes

.. NOTE::
    Lab instructions are written as if the student is executing the steps
    from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.


View Trading App Current State
---------------------------------

#. In Chrome, open a tab and go ``http://trading.acmefinancial.net``. Click the **Login** button. 
   This is an example "trading" application.

   .. image:: ./media/M2L2tradingGen.png
      :width: 800

#. Login to the application with the specified credentials. 

   +-------------------------+----------------------+
   |        Username         |      Password        |
   +=========================+======================+
   |  matt                   |  ``ilovef5``         |
   +-------------------------+----------------------+

   .. image:: ./media/M2L2tradingLogin.png
      :width: 200

   .. NOTE::
      Notice the "Coming Soon" for the "Quick Money Transfer" frame on the right.

   .. image:: ./media/M2L2trading1.png
      :width: 200

Deploy a Component using Postman
---------------------------------

#. On the jumphost, open **Postman**. Expand the **_NGINX Controller 3.x
   UDF (master)** Collection.

   .. image:: ./media/M2L2PMcoll.png
      :width: 400

#. Expand **Common Tasks**, **Admin Logon**, and select the **Login to Controller
   – admin – local** request.

   .. image:: ./media/M2L2PMcoll2.png
      :width: 400

#. In Postman select **Send**.

   .. image:: ./media/M2L2PMsend1.png
      :width: 600

   .. NOTE::
      Controller responds with a "204 No Content" response and an authentication cookie. 
      Postman uses this cookie for authentication in subsequent requests.

   .. image:: ./media/M2L2PMcookie.png
      :width: 400

#. Expand the **Retail-Development Environment**, **Application - trading** folder. 
   Open the **Application trading** subfolder and select the request name **4) Create Component
   – transfers**.

   .. image:: ./media/M2L2PMtransfer.png
      :width: 400

#. Click the **Body** view in the Postman request area. Look over the PUT request payload. 
   The JSON properties under ``desiredState``, ``logging``, ``security``, and ``backend`` 
   should look familiar based on the Component you deployed in the previous lab.

   .. image:: ./media/M2L2PMbody.png
      :width: 400

#. In Postman select **Send**.

   .. image:: ./media/M2L2PMsend2.png
      :width: 800

   .. NOTE::
      Controller follows an "eventual consistency model". The API responded to the Postman request with a "202 Accepted" status code.
      Controller is now working to bring about the desired state. 

   .. image:: ./media/M2L2PMconfig.png
      :width: 600

Verify Trading App Changes
---------------------------

#. In Chrome, reload the ``http://trading.acmefinancial.net/trading/index.php`` site.
   Verify the “Quick Money Transfer” is active and “Coming Soon” has been replaced.

   .. image:: ./media/M2L2result.png
      :width: 400


.. _loadgen:

Start WAF Traffic Generation for Analytics
-------------------------------------------

.. IMPORTANT::
   This step **MUST** be completed for statistics to be available in Module 3. 

#. Login to the "loadgen-1" instance. Using "PuTTY" select the **loadgen-1** saved session and click **Open**.

   .. image:: ./media/M2L2loadgenssh.png
      :width: 400

   .. IMPORTANT::
      If you receive a PuTTY warning regarding the server's host key click **Yes** to connect.
      This is caused by a unique host key being generated for each UDF deployment.

#. Execute the following "docker" command to generate traffic against the demo application deployed in this lab.

   .. code-block:: bash

      $ sudo docker start 89

#. The result of the command should echo the container name ("89").

   .. image:: ./media/M2L2loadgenresult.png
      :width: 600
