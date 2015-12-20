# ws-deploy

Vagrant + Ansible to configure Debian

## Usage

### Create your host variables

#### Set your login

    python -c \
        "usr = raw_input('clear_text_username: ');\
         f = open('host_vars/default/vault', 'w');\
         f.write('vault_user: %s\n' % usr);\
         f.close();\
        "

#### Set your login password

    python -c \
        "from passlib.hash import sha512_crypt;\
         pwd = sha512_crypt.encrypt(raw_input('clear_text_password: '));\
         f = open('host_vars/default/vault', 'a');\
         f.write('vault_password: %s\n' % pwd);\
         f.close();\
        "

### Encrypt your secrets

    ansible-vault encrypt host_vars/default/vault

### RAX Only

Follow steps in rax/roles/README.md

    git submodule init
    git submodule update
    less roles/rax/README.md

### Build your VM

    cd vagrant
    vagrant up
