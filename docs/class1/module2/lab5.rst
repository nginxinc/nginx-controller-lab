Lab 5 - Defining a specific listen IP
#######################################

The goal of this lab is to familiarize the student with configuring a specific listen IP for a Gateway.
There are times when it is desired to segment or prioritize traffic by using a specific IP of an NGINX Instance.  
This is necessary when enabling data plane high availability or when segmenting traffic via IP address on the NGINX Plus instance.

.. IMPORTANT::
    Estimated completion time: 5 minutes

.. NOTE::
    Lab instructions are written as if the student is executing the steps
    from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.


Defining the listen IP of a Gateway
-----------------------------------
#. The jumphost should already have Chrome loaded with the controller UI at the login screen:

   .. image:: ../media/ControllerLogin.png
      :width: 400

#. If not, open Chrome Browser.

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

#. Navigate to the **Services** section. The items or "tiles" under this menu will be used to create the configuration for this lab.

   .. image:: ../media/Tile-Services.png
      :width: 200

Create a Gateway
^^^^^^^^^^^^^^^^^

#. Select the "Gateways" tile.

   .. image:: ./media/M2L1GatewayTile.png
      :width: 200

#. Click the "Create" button in the upper right.

   .. image:: ./media/M2L1GWcreate.png
      :width: 600

#. Under the **Configuration** dialogue, fill out the form. When finished click **Next** or click the name of the next section.

   +---------------------+----------------------------------+
   |        Field        |      Value                       |
   +=====================+==================================+
   |  Name               | ``specialapp``                   |
   +---------------------+----------------------------------+
   |  Environment        | ``Echo Environment``             |
   +---------------------+----------------------------------+

   .. image:: ./media/M2L5GWDialogue.png
      :width: 600

#. Under the **Placements** dialogue, select the "Development NGINX West 03 (CAS)” Instance Ref.

   .. image:: ./media/M2L1Place.png
      :width: 700

#. Under the **Placements** dialogue, enter the "10.1.20.213” Listen IP.

   .. image:: ./media/M2L5Place.png
      :width: 700

   .. NOTE::
      This is a secondary IP that has already defined on the "Development NGINX West 03 (CAS)” machine. You can observe this In the IP Address field of the Instance in the **Infrastructure** section of Controller.

#. Under the **Hostnames** dialogue, leave the Hostname empty. 
   This implies that you will later define the Hostname in the URI setting of the Component or treat all traffic directed to this IP identically such as a TCP / UDP Component.

   .. image:: ./media/M2L5Hostnames.png
      :width: 700

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100

Create a Component
^^^^^^^^^^^^^^^^^^^

#. Using the echoapp: Select the "Components" section followed by the "Create Component" button in the top right.

   .. image:: ./media/M2L1CreateComponent.png
      :width: 800

#. Fill out the form and select the **Gateway Refs** from the drop-down.

   +-------------------------+--------------------------+
   |        Field            |      Value               |
   +=========================+==========================+
   |  Name                   | ``wildcard``             |
   +-------------------------+--------------------------+
   |  Gateway Refs           | ``specialapp``           |
   +-------------------------+--------------------------+

   .. image:: ./media/M2L5CompDiag.png
      :width: 700

#. Under the **URIs** dialogue, add the URI ``http://.*:8080`` and specify the ``REGEX`` **Match Method**.

   .. image:: ./media/M2L5CompURI.png
      :width: 700

   .. NOTE::
      If the port 8080 is not defined an error will be returned ``ListenIP 10.1.20.213 on Port 80 conflicts with an existing gateway``.
      This happens because other Gateways associated with the same instance are listening on all IP Addresses because the Listen IP was not defined.

#. Under the **Workload Groups** dialogue, fill out the form.

   +-------------------------+-----------------------------+
   |        Field            |      Value                  |
   +=========================+=============================+
   |  Name                   | ``wildcard Backend``        |
   +-------------------------+-----------------------------+
   |  Backend Workload URIs  | ``http://10.1.20.21:8001``  |
   +-------------------------+-----------------------------+

   .. image:: ./media/M2L5WGdiag.png
      :width: 600

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100

Test the Listen IP Component
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. In Chrome on ``jumphost-1``, open a new tab and enable "Developer Tools". 

   .. image:: ./media/M2L1DevTools.png
      :width: 900

#. Browse to the App URLs you created earlier (``http://10.1.20.213:8080``) to verify the "echo" application is functioning.

   .. image:: ./media/M2L1DevTools2.png
      :width: 800 

   .. NOTE::
      Using the REGEX expression of ``.*`` allowed the URI to match any hostname, even an IP address.
