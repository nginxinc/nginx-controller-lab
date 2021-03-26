Lab 1 - GUI ADC App Creation
#######################################

The goal of this lab is to familiarize the student with the NGINX Controller object model and concepts regarding ADC services.
The "app-centric" model used by Controller is a departure from both the BIG-IP's "network-centric" model and NGINX's config driven model.

.. IMPORTANT::
    Estimated completion time: 15 minutes

.. NOTE::
    Lab instructions are written as if the student is executing the steps
    from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.

Controller Object Model Concepts
---------------------------------
This section will cover NGINX Controller objects and attempt to compare them with known BIG-IP and NGINX concepts and nomenclature.

   .. image:: ./media/M2L1ServOver.png
      :width: 600

Environments
^^^^^^^^^^^^

An "Environment" is a logical grouping of Apps. It's used as a top-level construct for Role Based Access Control.
Environments are organizational in nature, therefore the concept is not represented in NGINX config deployed to managed NGINX Plus instances.
Conceptually, an environment is similar to a BIG-IP administrative partition.

Cert
^^^^

SSL certificates and keys are stored in a centralized Controller repository. 
They can then be assigned to specific "Gateways" as needed by the requested configuration.

Gateway
^^^^^^^

A "Gateway" is a collection of NGINX config directives deployed to a target NGINX Plus instance. 
This includes an FQDN for ingress, allowed HTTP methods, SSL/TLS config, and some advanced HTTP parameters (buffers, body size, TCP keepalives). 
These directives would be found in the "server" block of an NGINX config. 
There are several overlapping BIG-IP concepts found in TCP, HTTP, and ClientSSL profiles. 

App
^^^

An "App" is the logical grouping of "Components" that represent the *whole* application in a microservices architecture.
Each "Component" in an "App" represents an individual microservice. 
As the object is a logical grouping, it's not represented in an NGINX Plus instances config.
Analogous BIG-IP family concepts include an AS3 tenant or a BIG-IQ "Application".

Component
^^^^^^^^^

A "Component" is the most basic representation of a single service. This includes URIs for ingress, a "Workload Group" to determine 
where backend traffic should be routed, HTTP manipulation rules (redirects, rewrites, header manipulation), logging config, etc.
Similar BIG-IP concepts include a "Virtual Server", a "Pool", limited features from "HTTP Profiles", "Local Traffic Policies", and "iRules".    


Workload Group
^^^^^^^^^^^^^^

A "Workload Group" is a collection of backend servers. NGINX config references this concept as an "upstream".
In BIG-IP terminology the group would be a "pool" and the individual members "pool members".


Deploy an Application
-----------------------
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

Create an Environment
^^^^^^^^^^^^^^^^^^^^^^

#. Select the "Environments" tile.

   .. image:: ./media/M2L1EnvTile.png
      :width: 200

#. Click the "Create" button in the upper right.

   .. image:: ./media/M2L1EnvCreate.png
      :width: 700

#. Fill out the form.

   +---------------------+------------------------------+
   |        Field        |      Value                   |
   +=====================+==============================+
   |  Name               |  ``echo``                    |
   +---------------------+------------------------------+
   |  Display Name       | ``Echo Environment``         |
   +---------------------+------------------------------+

   .. image:: ./media/M2L1EnvDialogue.png
      :width: 700

3. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100


Add a Certificate
^^^^^^^^^^^^^^^^^

#. Select the "Certs" tile.

   .. image:: ./media/M2L1Certs.png
      :width: 200

#. Click the "Create" button in the upper right.

   .. image:: ./media/M2L1CertCreate.png
      :width: 800

#. Fill out the form and select the appropriate **Environment** from the drop-down. 

   +-----------------+----------------------------------+
   |        Field    |      Value                       |
   +=================+==================================+
   |  Name           |  ``echoapp.net``                 |
   +-----------------+----------------------------------+
   |  Environment    | ``Echo Environment``             |
   +-----------------+----------------------------------+

   .. image:: ./media/M2L1CertDialogue1.png
      :width: 700

#. Select the **Import PEM or PKC12** radio button and **Browse** for the cert and key.

   .. image:: ./media/M2L1CertDialogue2.png
      :width: 700

   The cert (**echoapp.net.crt**) and key (**echoapp.net.key**) can be found in **This PC -> Documents -> Certs** on "jumphost-1". 

   .. NOTE::
      You will need to browse and upload the cert and key individually as Controller does not allow simultaneous file uploads.

   .. image:: ./media/M2L1Cert&Key.png
      :width: 700

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100


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
   |  Name               |  ``echoappgw``                   |
   +---------------------+----------------------------------+
   |  Environment        | ``Echo Environment``             |
   +---------------------+----------------------------------+

   .. image:: ./media/M2L1GWDialogue.png
      :width: 600

#. Under the **Placements** dialogue, select the "Development NGINX West 03 (CAS)” Instance Ref.

   .. image:: ./media/M2L1Place.png
      :width: 700

#. Under the **Hostnames** dialogue, add the specified hostnames (``http://echoapp.net``, ``https://echoapp.net``). Do not specify a **Match Method** for either hostname. 
   Select the **echoapp.net** "Cert Reference".
   
   .. NOTE::
      You will need to use the **Add Hostname** link pictured below to add multiple hostnames.

   .. image:: ./media/M2L1Hostnames.png
      :width: 700

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100

Create an App
^^^^^^^^^^^^^

#. Select the "Apps" tile.

   .. image:: ../media/Services-Apps.png
      :width: 200

#. Click the "Create" button in the upper right.

   .. image:: ./media/M2L1AppsCreate.png
      :width: 600

#. Fill out the form and select the **Environment** from the drop-down.

   +---------------------+------------------------------+
   |        Field        |      Value                   |
   +=====================+==============================+
   |  Name               |  ``echoapp``                 |
   +---------------------+------------------------------+
   |  Environment        | ``Echo Environment``         |
   +---------------------+------------------------------+

   .. image:: ./media/M2L1Appdiag.png
      :width: 800

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100

Create a Component
^^^^^^^^^^^^^^^^^^^

#. Select the "Components" section followed by the "Create Component" button in center dialogue.

   .. image:: ./media/M2L1CreateComponent.png
      :width: 800

#. Fill out the form and select the **Gateway Refs** from the drop-down.

   +-------------------------+--------------------------+
   |        Field            |      Value               |
   +=========================+==========================+
   |  Name                   | ``echoappcomponent``     |
   +-------------------------+--------------------------+
   |  Gateway Refs           | ``echoappgw``            |
   +-------------------------+--------------------------+

   .. image:: ./media/M2L1CompDiag.png
      :width: 700

#. Under the **URIs** dialogue, add the URI "/". Do not specify a **Match Method**.

   .. image:: ./media/M2L1CompURI.png
      :width: 700

#. Under the **Workload Groups** dialogue, fill out the form.

   +-------------------------+-----------------------------+
   |        Field            |      Value                  |
   +=========================+=============================+
   |  Name                   | ``Echo Backend``            |
   +-------------------------+-----------------------------+
   |  Backend Workload URIs  | ``http://10.1.20.11:8000``  |
   +-------------------------+-----------------------------+

   .. image:: ./media/M2L1WGdiag.png
      :width: 600

#. Click **Submit** to complete.

   .. image:: ../media/Submit.png
      :width: 100

Test the Echo Application
^^^^^^^^^^^^^^^^^^^^^^^^^^

#. In Chrome on ``jumphost-1``, open a new tab and enable "Developer Tools". 

   .. image:: ./media/M2L1DevTools.png
      :width: 900

#. Browse to the App URLs you created earlier (``http://echoapp.net`` and ``https://echoapp.net``) to verify the "echo" application is functioning.
   Select the **echoapp.net** request to view the results.

   .. NOTE::
      This simple web application will "echo" back information about the HTTP request it is responding to.

   .. image:: ./media/M2L1DevTools2.png
      :width: 800 
