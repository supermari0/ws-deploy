# ws-deploy

to do:
- automatically install and configure i3 with Mod1 key
- automatically install and setup gnome-terminal as default

Vagrant + Ansible to configure Debian

## Usage

### Create your host variables

#### Set your login

    python -c \
        "usr = raw_input('username: ');\
         f = open('host_vars/default/vault', 'a');\
         f.write('vault_user: %s\n' % usr);\
         f.close();\
        "

#### Set your real name

    python -c \
        "usr = raw_input('fullname: ');\
         f = open('host_vars/default/vault', 'a');\
         f.write('vault_real_name: %s\n' % usr);\
         f.close();\
        "

#### Set your email

    python -c \
        "usr = raw_input('email: ');\
         f = open('host_vars/default/vault', 'a');\
         f.write('vault_email: %s\n' % usr);\
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

### Add your gpg keys

EITHER: Remove the gpg-keys role from setup.yml
OR: Add your ASCII armored keys to `host_vars/default/vault-test`:

    vault_gpg_private_key: |
      -----BEGIN PGP PRIVATE KEY BLOCK-----
      <your_private_key>
      -----END PGP PRIVATE KEY BLOCK-----

    vault_gpg_public_key: |
      -----BEGIN PGP PUBLIC KEY BLOCK-----
      <your_private_key>
      -----END PGP PUBLIC KEY BLOCK-----

### Add your ssh keys

EITHER: Remove the ssh-keys role from setup.yml
OR: Add your keys to `host_vars/default/vault-test`:

    vault_ssh_private_key: |
      -----BEGIN RSA PRIVATE KEY-----
      <your_private_key>
      -----END RSA PRIVATE KEY-----

    vault_ssh_public_key: <your_public_key>

### Encrypt your secrets

    ansible-vault encrypt host_vars/default/vault

### Build your VM

    cd vagrant
    vagrant up
