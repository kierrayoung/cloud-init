.. _datasource_ibmcloud:

IBM Cloud
*********

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


Configuration Settings
The following configuration can be changed for 
