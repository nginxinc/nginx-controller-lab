Lab 2 - NGINX Controller Resiliency
############################################

The goal of this lab is to add another host as a third member to an NGINX Controller cluster. 

.. IMPORTANT::
   - Estimated completion time: 10 minutes

.. NOTE::
     Lab instructions are written as if the student is executing the steps
     from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.


Create an additional NGINX Controller Node
------------------------------------------

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

#. Navigate to the **Platform** section.

   .. image:: ./media/M1L1Platform.png
      :width: 200

#. Open the **Cluster** tile.

   .. image:: ./media/M1L2ClusterTileSmall.png
      :width: 600

#. View the current "Cluster Configuration".

   .. image:: ./media/M1L2ClusterConfig.png
      :width: 800

.. NOTE::
     The "Cluster Configuration" section indicates this Controller instance is part of a cluster.
     The "FQDN" is used as the common name for the cert applied to API Gateway pod -- 
     ie. the service that exposes API endpoints and the GUI.

.. IMPORTANT::
      The "load balancer" option will be configurable in a future Controller release.
      See this lab's Additional :ref:`Reference` for more details.

.. NOTE::
      The "Nodes" section shows the cluster currently has 2 Controller instances -- 
      "ip-10-1-1-5.us-west-2.compute.internal" (or the "controller-1" UDF instance where you are logged in)
      and the UDF instance "controller-2". 

#. Click the **Create Node** button in the upper right.

   .. image:: ./media/M1L2CreateNodeButton.png
      :width: 200

#. Walk through the dialogue to add the "controller-3" UDF instance by specifying a "Name" and the "Hostname or IP Address".
   Click the **Save** button.

   +-------------------------+-------------------+
   |        Field            |      Value        |
   +=========================+===================+
   |  Name                   |  ``controller-3`` |
   +-------------------------+-------------------+
   |  Hostname or IP         |  ``10.1.1.10``    |
   +-------------------------+-------------------+

   .. image:: ./media/M1L2CreateNodeDialogue.png
      :width: 800

#. **View** the installation instructions. Copy the install command and "join key" to your clipboard. 

   .. image:: ./media/M1L2NodeViewButton.png
      :width: 800

   .. image:: ./media/M1L2NodeJoinCommand.png
      :width: 800

Run the install command to join the instance to the cluster
-----------------------------------------------------------

#. Login to the "controller-3" instance. Using "PuTTY" select the **controller-3** saved session and then click **Open**.

   .. image:: ./media/M1L2puttyc3.png
      :width: 400

   .. IMPORTANT::
      If you receive a PuTTY warning regarding the server's host key click **Yes** to connect.
      This is caused by a unique host key being generated for each UDF deployment.

#. Execute the install.sh command from the installer directory. Answer "y" (ie. "yes") to the prompts.

   .. code-block:: bash

      $ cd controller-installer/
      $ ./install.sh --join-key {{base64 encoded key}}

   .. image:: ./media/M1L2InstallCommand.png
      :width: 800

   #. The result of the command should eventually show the node was successfully joined to the cluster.

   .. image:: ./media/M1L2NodeJoinSuccess.png
      :width: 300

View the results
----------------

#. In Chrome, view the "Cluster Configuration" from the **Cluster** tile.

   .. image:: ./media/M1L2NodesConfigured.png
      :width: 800

(Optional) Explore the Kubernetes Cluster
------------------------------------------

If you're familiar with Kubernetes (k8s), you can look at the k8s cluster created by NGINX Controller for resiliency purposes.  

#. Use your existing PuTTY session to "controller-3" or create a new session to one of the Controller instances. 

   .. image:: ./media/M1L2puttyc1.png
      :width: 400

   .. IMPORTANT::
      If you receive a PuTTY warning regarding the server's host key click **Yes** to connect.
      This is caused by a unique host key being generated for each UDF deployment.


#. View the cluster nodes.

   .. code-block:: shell

      kubectl get nodes 

   .. image:: ./media/M1L2Nodes.png
      :width: 800

   .. NOTE::
      The command's output shows there are three nodes in this k8s cluster.


#. View the deployed pods.

   .. code-block:: shell

      kubectl get pods -n nginx-controller -o wide
      
   .. image:: ./media/M1L2K8s.png
      :width: 1024

   .. NOTE::
      The command's output shows Controller's several pods are distributed among the three nodes (the "NODE" column).


.. _Reference:

Additional Reference
--------------------
Future NGINX Controller releases will allow for the creation of a floating self-ip by adding a "load balancer" to the
exposed API Gateway ("apigw") Kubernetes service. For on-premise installations `MetalLB`_ handle L2 failover. 
For cloud installations a k8s service with type `LoadBalancer`_, resulting in a cloud native external load balancer, will be used.

.. _MetalLB: https://metallb.universe.tf/
.. _LoadBalancer: https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer
