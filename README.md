# ws-deploy

Vagrant + Ansible to configure Debian

## Usage

    # Create your inventory file
    echo "<ip_address> user=<user_account_name>" > hosts

    # RAX Only (follow steps in rax/roles/README.md)
    git submodule init
    git submodule update
    less roles/rax/README.md

    # Build your VM
    cd vagrant
    vagrant up
