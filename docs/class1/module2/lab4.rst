Lab 4 - TCP Load Balancing / Routing
######################################################

The goal of this lab is to demonstrate a layer 4 or TCP load balancer configuration.  
Not all traffic is HTTP, and though there is a large number of ways to manipulate HTTP traffic, sometimes you also have to route TCP or UDP traffic. 

.. important::
   - Estimated completion time: 5 minutes

.. NOTE::
     Lab instructions are written as if the student is executing the steps
     from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.

Access the App Component
-------------------------

#. Open Chrome Browser.
#. Access the NGINX Controller UI through the provided bookmark.

   .. image:: ../media/ControllerBookmark.png
      :width: 600

#. Login with the ``Peter Parker`` account who is an NGINX Controller admin.

   +-------------------------+-----------------+
   |      Username           |    Password     |
   +=========================+=================+
   | peter@acmefinancial.net | ``Peter123!@#`` |
   +-------------------------+-----------------+

   .. image:: ../media/ControllerLogin-Peter.png
      :width: 400

#. Navigate to the **Services** section.

   .. image:: ../media/Tile-Services.png
      :width: 200

#. Select the "Apps" tile.

   .. image:: ../media/Services-Apps.png
      :width: 200

#. Select the **echoapp** from the "Echo Environment" you created in Module 2 Lab 1.

   .. image:: ./media/M2L3echoapp.png
      :width: 200

Create a TCP Component
----------------------

#. Using the echoapp:  Select the "Components" section followed by the "Create Component" button in the top right.

   .. image:: ./media/M2L1CreateComponent.png
      :width: 800

#. Fill out the form and select the **Gateway Refs** from the drop-down.

   +-------------------------+--------------------------+
   |        Field            |      Value               |
   +=========================+==========================+
   |  Component Type         | TCP/UDP                  |
   +-------------------------+--------------------------+
   |  Name                   | ``echoapptcp``           |
   +-------------------------+--------------------------+
   |  Gateway Refs           | ``echoappgw``            |
   +-------------------------+--------------------------+

   .. image:: ./media/M2L4CompDiag.png
      :width: 700

#. Under the **URIs** dialogue, add the URI ``tcp://*:9443``

   .. image:: ./media/M2L4CompURI.png
      :width: 700

#. Under the **Workload Groups** dialogue, fill out the form.

   +-------------------------+-----------------------------+
   |        Field            |      Value                  |
   +=========================+=============================+
   |  Name                   | ``TCP Backend``             |
   +-------------------------+-----------------------------+
   |  Backend Workload URIs  | ``tcp://10.1.20.21:8000``   |
   +-------------------------+-----------------------------+
   |  Backend Workload URIs  | ``tcp://10.1.20.11:8000``   |
   +-------------------------+-----------------------------+

   .. image:: ./media/M2L4WGdiag.png
      :width: 600

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100

Test the TCP Component
^^^^^^^^^^^^^^^^^^^^^^
#. In Chrome on ``jumphost-1``, open a new tab and enable "Developer Tools". 

   .. image:: ./media/M2L1DevTools.png
      :width: 900

#. Browse to the App URLs you created earlier with the new port (``http://echoapp.net:9443`` ) to verify the "echo" application is functioning over TCP.
   Select the **echoapp.net** request to view the results.

   .. NOTE::
      This simple web application will "echo" back information about the HTTP request it is responding to.

   .. image:: ./media/M2L1DevTools2.png
      :width: 800 

#. Browse to the same URL using HTTPS (``https://echoapp.net:9443`` ) to verify the "echo" application is functioning over TCP.
   Notice that the traffic is blocked.
   If you wanted to encrypt the TCP traffic, you would provide a certificate and define the protocol as ``tcp+tls`` instead of ``tcp`` then like HTTPS traffic the Gateway would be providing SSL Offload before forwarding to the backend workloads.

   .. image:: ./media/M2L4DevTools2.png
      :width: 400 


Additional Reference
--------------------

The "TCP/UDP" component allows configuration of stream or Layer 4 proxy.
These features are powered by the NGINX `stream`_ module. Review the module documentation for more information. 



.. _stream: http://nginx.org/en/docs/stream/ngx_stream_core_module.html
