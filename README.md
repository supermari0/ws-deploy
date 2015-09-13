# ws-deploy

Ansible to configure Debian

## Usage

    # Create your inventory file
    echo "<ip_address> user=<user_account_name>" > hosts

    # Set your remote authorized key file for ssh
    ansible-playbook -c paramiko -i hosts init.yml --ask-pass

    # Setup your remote host(s)
    ansible-playbook -i hosts setup.yml
