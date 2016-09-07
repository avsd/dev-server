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

## Troubleshooting

1. NodeJS installation fires an error during the deployment process:

            TASK [nodesource.node : Install Node.js] ***************************************
            fatal: [localhost]: FAILED! => {"cache_update_time": 1473216695, "cache_updated": true,
                   "changed": false, "failed": true, "msg": "'/usr/bin/apt-get -y
                   -o \"Dpkg::Options::=--force-confdef\" -o \"Dpkg::Options::=--force-confold\"
                       install 'nodejs=4.4*'' failed: E: Version '4.4*' for 'nodejs' was not found\n",
                   "stderr": "E: Version '4.4*' for 'nodejs' was not found\n",
            ...

   There might be a mismatch between the NodeJS version in the Ansible package and available
   versions in Ubuntu repository. You just need to add a correct version as an environment
   variable. For Ubuntu 16.4 it will be:

            -e nodejs_version=4.5

   To check which versions are available run the command:

            apt-cache showpkg nodejs | grep Versions -A10

2. VIM shows errors when opened.

   You may want to install Vim plugins manually, as it does not always work:
   
   1. Run Vim
   2. Ignore the errors it shows
   3. Run the Vim command: ``:PluginInstall``
