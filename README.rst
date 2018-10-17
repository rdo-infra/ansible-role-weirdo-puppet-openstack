ansible-role-weirdo-puppet-openstack
------------------------------------
This role provides an implementation of the
puppet-openstack-integration_ gate jobs for
the WeIRDO_ project.

.. _puppet-openstack-integration: https://github.com/openstack/puppet-openstack-integration
.. _WeIRDO: https://github.com/redhat-openstack/weirdo

Supported gate jobs
~~~~~~~~~~~~~~~~~~~

* gate-puppet-openstack-integration-scenario001-dsvm-centos7
* gate-puppet-openstack-integration-scenario002-dsvm-centos7
* gate-puppet-openstack-integration-scenario003-dsvm-centos7

Role variables
~~~~~~~~~~~~~~

For default values, see `defaults/main.yml`_

* ``project``: Name of the project, analogous to the role name
* ``openstack_release``: Name of the OpenStack release to select which trunk repository to use by default
* ``version``: Version/tag/branch of puppet-openstack-integration to clone
* ``manage_repos``: Whether puppet-openstack-integration should manage repository setup
* ``repository``: URL to the puppet-openstack-integration repository
* ``clone_path``: Path where puppet-openstack-integration will be cloned
* ``delorean_url``: URL to the delorean repository .repo file.
* ``delorean_deps_url``: URL to the delorean-deps repository .repo file.
* ``copy_puppet_logs_url``: URL to the copy_puppet_logs.sh script for puppet-openstack-integration log retrieval
* ``puppet_workspace``: Path where puppet-openstack-integration should believe the jenkins workspace is at
* ``required_packages``: Required packaged dependencies to install prior to running the tests
* ``gem_packages``: Required packaged gems to install prior to running the tests
* ``nested_virtualization``: When set to true, it will enable nested virtualization in the system based on availability

.. _defaults/main.yml: https://github.com/redhat-openstack/ansible-role-weirdo-puppet-openstack/blob/master/defaults/main.yml

Included tasks
~~~~~~~~~~~~~~

* ``repositories``: Ensures required repositories are setup
* ``packages``: Ensures required dependencies are installed
* ``setup``: Clones the puppet-openstack-integration repository and prepares log retrieval
* ``logs``: Retrieves logs with the copy_puppet_logs.sh script
* ``run``: Runs the integration tests

Dependencies
~~~~~~~~~~~~

`ansible-role-weirdo-common`_ to be installed as ``common``

.. _ansible-role-weirdo-common: https://github.com/redhat-openstack/ansible-role-weirdo-common

Example playbook
~~~~~~~~~~~~~~~~

.. code-block:: yaml

    - name: Run puppet-openstack-integration scenario001 tests
      hosts: openstack_nodes
      force_handlers: True
      roles:
        - { role: "puppet-openstack", test: "scenario001" }
