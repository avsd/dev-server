# dev-server-playbook

## When using without OpenStack:


1. Create an Ubuntu instance
2. SSH to the instance and install the latest release of Ansible and Git:

        $ sudo apt-get install software-properties-common
        $ sudo apt-add-repository ppa:ansible/ansible
        $ sudo apt-get update
        $ sudo apt-get install ansible git

3. Add following two lines to ``/etc/ansible/hosts``:

        [localhost]
        localhost

4. Clone the repository and ``cd`` into it:

        $ git clone https://github.com/avsd/dev-server.git
        $ cd dev-server

5. Install ``nodesource-node`` role using Ansible Galaxy:

        $ sudo ansible-galaxy install nodesource.node

6. Run the playbook:

        $ sudo ansible-playbook \
            -c local \
            -e username=<your-desired-username> \
            -e email=<your@email> \
            -e fullname=<your-fullname> \
            playbook.yml

You may want to install Vim plugins manually, as it does not always work:

1. Run Vim
2. Ignore the errors it shows
3. Run the Vim command: ``:PluginInstall``
