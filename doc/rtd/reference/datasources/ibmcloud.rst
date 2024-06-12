.. _datasource_ibmcloud:

IBM Cloud
*********
When an IBM instance starts, cloud-init is launched on its default eth0 address, where it then reads the
relevant user and metadata to set up the instance.

Metadata is accessible via the following URL:

.. code-block:: sh

    curl -X GET "http://169.254.169.254/metadata/v1/instance?version=2022-03-01"    
    -H "Accept: application/json"    
    -H "Authorization: Bearer $instance_identity_token"    
    | jq -r

User metadata is specified on instance creation, and is accessible via the following URL:

.. code-block:: sh

    curl -X GET "http://169.254.169.254/metadata/v1/instance/initialization?version=2022-03-01"    
    -H "Accept: application/json"    
    -H "Authorization: Bearer $instance_identity_token"    
    | jq -r

Configuration settings
======================

The following configuration can be set for the datasource in the system
configuration (in :file:`/etc/cloud/cloud.cfg`).

The settings that may be configured are:

``datasource_list``
-----------------

This is a list of any external data sources to be crawled for information. 
Available options are:
====
* Box
* IBM Cloud Object Storage
* Microsoft SharePoint Online
* Microsoft SharePoint On Prem
* Salesforce
* Web crawl
..

`` distro``
-----------------
This setting affects which distribution is used. Certain distributions may have different requirements or settings for initialization;
please check the IBM documentation, linked below, to ensure that the image is set up correctly.

``paths``
-----------------
Information here is passed to the paths or distro classes as appropriate.


(`Additional information and resources can be found at the CloudIBM documentation here. <https://cloud.ibm.com/docs>`_)
