# ws-deploy

Ansible to configure Debian

## Usage


    # Create your inventory file
    echo "<ip_address> user=<user_account_name> rax=no" > hosts

    # RAX Only (follow steps in rax/roles/README.md)
    git submodule init
    git submodule update
    less roles/rax/README.md

    # Set your remote authorized key file for ssh
    ssh-copy-id root@<ip_address>

    # Setup your remote host(s)
    ansible-playbook -i hosts setup.yml
