====================
Adding a new Gateway
====================

Add a Gateway using the GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   1. In the Controller GUI tab of the web browser
   2. Select the Services menu from the navigation bar
   3. Select Gateways
   4. Select Overview
   5. Select |create|
   6. Enter the Name: trading-api.acmefinancial.net
   7. Select the environment:  Retail Dev
   8. Select Next
   9. Select the Instance Reference: dev-nginx-1
   10. Select Next
   11. Add the URI: https://trading-api.acmefinancial.net
   12. Select Done
   13. For the Certificate Reference select |createNew|
   14. Name the new certificate: trading-api.acmefinancial.net
   15. Browse to the trading-api.dev.acmefinancial.net.crt certificate
   16. Browse to the trading-api.dev.acmefinancial.net.key key
   17. Select Submit to create the new certificate
   18. Select Next
   19. Select Next
   20. Select Publish
   21. Note that the Gateway progresses from a state of configuring to configured.

Certificates (PEM or PKCS12) can be imported into Controller at the time they are added to a Gateway or Component, they can be defined and managed seperately (such as by a unique certificate team) and only referenced, or a file path local to the NGINX instance can be defined.  All giving unique flexibility to David and Samantha in best meeting how they want to manage their certificates.

.. |create| image:: ../../_static/create.png

.. |createNew| image:: ../../_static/create_new.png