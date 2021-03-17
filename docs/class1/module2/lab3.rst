Lab 3 - Advanced ADC Features
######################################################

The goal of this lab is to demonstrate a few "advanced ADC" features which are now included in NGINX Controller. Previously, these
features were only available as NGINX config directives. 

.. important::
   - Estimated completion time: 10 minutes

.. NOTE::
     Lab instructions are written as if the student is executing the steps
     from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.

Access the App Component
-------------------------

#. Open Chrome Browser.
#. Access the NGINX Controller UI through the provided bookmark.

   .. image:: ./media/M1L1ControllerBookmark.png
      :width: 400

#. Login with the ``Peter Parker`` account who is an NGINX Controller admin.

   +-------------------------+-----------------+
   |      Username           |    Password     |
   +=========================+=================+
   | peter@acmefinancial.net | ``Peter123!@#`` |
   +-------------------------+-----------------+

   .. image:: ./media/M1L1ControllerLogin.png
      :width: 400

#. Navigate to the **Services** section, and select the **Apps** tile.

   .. image:: ./media/M2L3ServicesTile.png
      :width: 200

   .. image:: ./media/M2L3AppsTile.png
      :width: 100

#. Select the **echoapp** from the "Echo Environment" you created in Module 2 Lab 1.

   .. image:: ./media/M2L3echoapp.png
      :width: 200

Create a URI Rewrite
---------------------

#. Navigate to **Components**. **Edit** the "echoappcomponent" you created earlier.

   .. image:: ./media/M2L3echoappEdit.png
      :width: 800

#. Under the "Advanced" section, select **Programmability**.

   .. image:: ./media/M2L3program.png
      :width: 600

#. In Chrome, test the response from the "echo" application before any changes are made to the component. 
   Using Chrome Developer tools like previously in this module, make a request to ``http://echoapp.net/example``.
   Note the response.

   .. image:: ./media/M2L3URLbar.png
      :width: 300 

   .. image:: ./media/M2L3beforeURLRW.png
      :width: 800

.. NOTE::
     The app's JSON response confirms that the request received was to ``path: "/example"``. 

#. On Controller, add a "URI Rewrite" to the component. This rewrite will seamlessly modify all requests to "/example*" to "/modified*".
   Click **Add URI Rewrites** from "Programmability" dialogue.

   .. image:: ./media/M2L3AddRW.png
      :width: 600

#. Complete the dialogue and click **Done** to save the rewrite. 
   The NGINX `rewrite`_ module, and the Controller implementation, use PCRE regular expression syntax.

   +-------------------------+-----------------------+
   |        Field            |      Value            |
   +=========================+=======================+
   | Incoming Pattern        |  ``~*^/example(.*)$`` |
   +-------------------------+-----------------------+
   | Rewrite Pattern         |  ``/modified$1``      |
   +-------------------------+-----------------------+

   .. image:: ./media/M2L3AddRWdialogue.png
      :width: 600

   .. image:: ./media/M2L3RWready.png
      :width: 600

   .. IMPORTANT::
     More advanced and ordered rulesets for URI modifications can be achieved through the use of the "After Execute" modifier.

#. Click **Submit** and verify the changes to the component are pushed to the "Gateway". The Component status should go from "Configuring" to "Configured". 

   .. image:: ./media/M2L3Submit.png
      :width: 200

   .. image:: ./media/M2L3RWconfigured.png
      :width: 800

#. In Chrome, Test the URI rewrite by sending another request to the echo application for "/example" (ie. just hit refresh on that tab). Observe the response.

   .. image:: ./media/M2L3afterURLRW.png
      :width: 800

   .. NOTE::
     The "echo" app's JSON response now shows it received a request for "/modified" as opposed to the URI in the browser bar ("/example").


Create a Request Header Modification
-------------------------------------

#. Back under the "echoapp" App in Controller, navigate to **Components**. **Edit** the "echoappcomponent" you created earlier.

   .. image:: ./media/M2L3echoappEdit.png
      :width: 800

#. Under the "Advanced" section, select **Programmability**.

   .. image:: ./media/M2L3program.png
      :width: 600

#. In Chrome, take note of the HTTP headers in the response from the previous requests to the "echo" app.

   .. image:: ./media/M2L3beforeHeaders.png
      :width: 800

#. On Controller, add a "Request Header Modification" to the component. This feature will inject an HTTP header into the request before it reaches the upstream/pool members.
   Click **Add Request Header Modification** from "Programmability" dialogue.

   .. image:: ./media/M2L3AddHM.png
      :width: 400

#. Complete the dialogue and click **Done** to save the rewrite. 

   +-------------------------+--------------------------------------+
   |        Field            |      Value                           |
   +=========================+======================================+
   | Action                  |  ``Add``                             |
   +-------------------------+--------------------------------------+
   | Header Name             |  ``X-Controller-Instance``           |
   +-------------------------+--------------------------------------+
   | Header Value            |  ``Development NGINX West 03 (CAS)`` |
   +-------------------------+--------------------------------------+

   .. image:: ./media/M2L3HeaderDialogue.png
      :width: 600

   .. image:: ./media/M2L3Headerready.png
      :width: 600

#. Click **Submit** and verify the changes to the component are pushed to the "Gateway". The Component status should go from "Configuring" to "Configured". 

   .. image:: ./media/M2L3Submit.png
      :width: 200

   .. image:: ./media/M2L3RWconfigured.png
      :width: 800

#. In Chrome, test the HTTP header insertion by sending another request to the echo application (ie. just hit refresh on that tab). Observe the response headers.

   .. image:: ./media/M2L3afterHM.png
      :width: 800

   .. NOTE::
     The "echo" app's JSON response shows the inserted header was added in the HTTP request.
     In this arbitrary example, we've added a header to show which NGINX Plus instance handled the request. 
     Request and Response HTTP headers can be added or deleted as needed by your application.

Additional Reference
--------------------

The "Programmability" section allows configuration of URI redirects, URI rewrites, request Header modifications, and response header modifications.
These features are powered by the NGINX `rewrite`_ module. Review the module documentation for more information. 



.. _rewrite: http://nginx.org/en/docs/http/ngx_http_rewrite_module.html
