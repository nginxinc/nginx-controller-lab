.. _overview:

F5 Labs - Index
=======================

Welcome
-------

Welcome to the |classbold| lab.


Getting Started
---------------

Please follow the instructions provided by the instructor to start your
lab. If you're viewing this lab guide, you've likely already started your UDF Course.

.. IMPORTANT::
	 All work for this lab can be performed exclusively from the Windows
	 jumphost. No installation or interaction with your local system is
	 required. 

Login to the "jumphost-1" UDF instance using the RDP Access method and the provided admin account.
This might look slightly different in the UDF courses interface.

   .. image:: ./class1/media/IntrojumpHostAccessMethod.png
      :width: 600

   +---------------+---------------+
   |   Username    |  Password     |
   +===============+===============+
   | Administrator | ``BZ8D8MCVR`` |
   +---------------+---------------+

Lab Topology
------------

The following components are included in the lab environment:

- 3 X NGINX Controller Instances (v3.x)
- 1 X Postgres Database Instance (used for NGINX Controller)
- 3 X NGINX Plus Instances w/ agents installed (CentOS 7)
- 1 X Application Servers (apps running in Docker on Ubuntu 18.04)
- 1 X Windows Domain Controller (Windows 2019 Server)
- 1 X Load Generator Instances (Ubuntu 18.04)


NGINX Controller Credentials
----------------------------

NGINX Controller is configured to perform authentication against the blueprint's
Active Directory Domain Controller. In this lab, you will use the following accounts:

.. list-table::
    :widths: 40 60 20 40
    :header-rows: 1
    :stub-columns: 1

    * - **Employee**
      - **Login UPN**
      - **Password**
      - **Active Directory Security Group**
    * - Peter Parker
      - peter@acmefinancial.net
      - ``Peter123!@#``
      - nginx-controller-admins
    * - Natasha Romanoff
      - natasha@acmefinancial.net
      - ``Natasha123!@#``
      - nginx-controller-user
    * - admin istrator (fallback account)
      - admin@acmefinancial.net
      - ``Admin123!@#``
      - NA/Local User

If using this blueprint outside of the lab and you'd like to explore NGINX Controller's RBAC implementation,
the following other accounts are available:

.. list-table::
    :widths: 40 60 20 40
    :header-rows: 1
    :stub-columns: 1

    * - **Employee**
      - **Login UPN**
      - **Password**
      - **Active Directory Security Group**
    * - Wanda Maximoff
      - wanda@acmefinancial.net
      - ``Wanda123!@#``
      - nginx-controller-admins
    * - Clint Barton
      - clint@acmefinancial.net
      - ``Clint123!@#``
      - nginx-controller-user
    * - Luke Cage
      - luke@acmefinancial.net
      - ``Luke123!@#``
      - nginx-controller-readers


.. toctree::
   :maxdepth: 3
   :caption: Lab Contents:
   :glob:

   class*/module*/module*
