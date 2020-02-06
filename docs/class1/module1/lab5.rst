===================================================
Add a Gateway for the mobile trading app
===================================================

+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| The trading app has been a great product for ACME Financial. It's currently available as a  |
| browser GUI. The business unit wants to expand this to a new mobile application so that     |
| retail customers can do trades on the go.                                                   |
| To enable a new mobile API for customers ACME Financial needs to expose a brand new gateway |
| to the public Internet, in order for Samantha's mobile app to receive API calls.            |
| When any new endpoint is exposed to the public Interney, ACME's standards require David get |
| involved to ensure security for API calls coming into the bank. Samantha will partner with  |
| David to ask for a new gateway, with a new certificate, to make sure that trading API       |
| interactions are secure.                                                                    |
| Let's work through the process of David establishing a new gateway for Samantha.            |
+---------------------------------------------------------------------------------------------+


Add a Gateway using the GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    1. Select the Controller GUI tab in Chrome on the Jumphost. Verify you are logged in as `admin` using the credentials:

      - username: `admin@acmefinancial.net`
      - password:  `Admin123!@#`
      
    2. Select the `Services` menu from the navigation bar
    3. Select `Gateways`
    4. Select |create|
    5. Enter the Name: `trading-api.acmefinancial.net`
    6. Select the environment:  `Retail Dev`
    7. Select `Next`
    8. Select the Instance Reference: `dev-nginx-1`
    9. Select `Next`
    10. Add the URI: `https://trading-api.acmefinancial.net`
    11. Select `Done`
    12. For the Certificate Reference, select |createNew|
    13. Name the new certificate: `trading-api.dev.acmefinancial.net`
    14. Browse to the trading-api.dev.acmefinancial.net.crt certificate (it's in your jumphost,  in Documents > Certs)
    15. Browse to the trading-api.dev.acmefinancial.net.key key (it's in your jumphost,  in Documents > Certs)
    16. Select `Submit` to create the new certificate
    17. Select `Next`
    18. Select `Next`
    19. Select `Publish`
    20. Note that the Gateway progresses from a state of "configuring" to "configured".


+---------------------------------------------------------------------------------------------+
| Talk Track                                                                                  |
+=============================================================================================+
| Certificates (PEM or PKCS12) can be imported into Controller at the time they're added to   |
| a Gateway or Component. They can be defined and managed separately (such as by a specific   |
| certificate/security team) with Controller only referencing them, or a file path local to   |
| NGINX instance can be defined.                                                              |
| These options give David and Samantha unique flexibility to enable how they want to manage  |
| their certificates.                                                                         |
+---------------------------------------------------------------------------------------------+

.. |create| image:: ../../_static/create.png

.. |createNew| image:: ../../_static/create_new.png
