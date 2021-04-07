Lab 6 - Launch Security Traffic Generation
################################################

The goal of this lab is to launch traffic generation for the security enabled data path.

.. NOTE::
    This is less of a lab exercise and more of ensuring your deployment is prepared for the next lab.
    This is critical to complete for the remaining exercises.

.. IMPORTANT::
    Estimated completion time: 5 minutes

.. NOTE::
    Lab instructions are written as if the student is executing the steps
    from the Windows jumphost -- ``jumphost-1``. See the :ref:`overview` for connection details.

    .. _loadgen:

Start WAF Traffic Generation for Analytics
-------------------------------------------

.. IMPORTANT::
   This step **MUST** be completed for statistics to be available in Module 3. 

#. Login to the "loadgen-1" instance. Using "PuTTY" select the **loadgen-1** saved session and click **Open**.

   .. image:: ./media/M2L6loadgenssh.png
      :width: 400

   .. IMPORTANT::
      If you receive a PuTTY warning regarding the server's host key click **Yes** to connect.
      This is caused by a unique host key being generated for each UDF deployment.

#. Execute the following "docker" command to generate traffic against the demo application deployed in this lab.

   .. code-block:: bash

      $ sudo docker start wrk_trading.acmefinancial.net-cas

#. The result of the command should echo the container name ("wrk_trading.acmefinancial.net-cas").

   .. image:: ./media/M2L6loadgenresult.png
      :width: 600
