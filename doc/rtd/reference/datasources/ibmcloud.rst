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

To pass this example script to ``cloud-init`` running in a  `RHEVm`_ v3.0 VM
set the "Custom Properties" when creating the RHEMv v3.0 VM to: ::

    floppyinject=user-data.txt:IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gSm9lISIgPj4gL3RtcC9KSlZfSm9lX291dC50eHQK

.. note::
   The prefix with file name must be: ``floppyinject=user-data.txt:``

It is also possible to launch a `RHEVm`_ v3.0 VM and pass optional user
data to it using the `Delta Cloud`_.

vSphere
=======

For VMWare's `vSphere`_ the user data is injected into the VM as an ISO
via the CD-ROM. This can be done using the `vSphere`_ dashboard
by connecting an ISO image to the CD/DVD drive.

To pass this example script to ``cloud-init`` running in a `vSphere`_ VM
set the CD/DVD drive when creating the vSphere VM to point to an
ISO on the data store.

.. note::
   The ISO must contain the user data.

For example, to pass the same ``simple_script.bash`` to vSphere:

Create the ISO
--------------

.. code-block:: sh

    $ mkdir my-iso

.. note::
   The file name on the ISO must be: ``user-data.txt``

.. code-block:: sh

    $ cp simple_script.bash my-iso/user-data.txt
    $ genisoimage -o user-data.iso -r my-iso

Verify the ISO
--------------

.. code-block:: sh

    $ sudo mkdir /media/vsphere_iso
    $ sudo mount -o loop user-data.iso /media/vsphere_iso
    $ cat /media/vsphere_iso/user-data.txt
    $ sudo umount /media/vsphere_iso

Then, launch the `vSphere`_ VM the ISO ``user-data.iso`` attached as a CD-ROM.

It is also possible to launch a `vSphere`_ VM and pass optional user
data to it using the Delta Cloud.

.. _RHEVm: https://www.redhat.com/virtualization/rhev/desktop/rhevm/
.. _vSphere: https://www.vmware.com/products/datacenter-virtualization/vsphere/overview.html
.. _Delta Cloud: http://deltacloud.apache.org
