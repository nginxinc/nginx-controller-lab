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

#. On the jumphost, open **Postman** if it is not currently running. The icon can be found on the desktop. Expand the **NGINX Controller 3.x** Collection.

   .. image:: ../media/PMcoll.png
      :width: 400

#. Expand **Common Tasks**, **Admin Logon**, and select the **Login to Controller
   – admin – local** request.

   .. image:: ../media/PMcoll2.png
      :width: 400

#. In Postman select **Send**.

   .. image:: ../media/PMsend1.png
      :width: 800

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
      :width: 700

#. In Postman select **Send**.

   .. image:: ./media/M2L2PMsend2.png
      :width: 800

   .. NOTE::
      Controller follows an "eventual consistency model". The API responded to the Postman request with a "202 Accepted" status code.
      Controller is now working to bring about the desired state. 

   .. image:: ./media/M2L2PMconfig.png
      :width: 700

Verify Trading App Changes
---------------------------

#. In Chrome, reload the ``http://trading.acmefinancial.net/trading/index.php`` site.
   Verify the “Quick Money Transfer” is active and “Coming Soon” has been replaced.

   .. image:: ./media/M2L2result.png
      :width: 400
