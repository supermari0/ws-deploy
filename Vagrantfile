# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "debian/contrib-jessie64"
  # TODO: checksum this

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "10.20.30.40"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "~/Documents/dev-vm-share", "/mnt/host-share"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Set the VM name
    vb.name = "mario_debian_dev"

    # Customize the number of CPUs
    vb.cpus = 1

    # Customize the amount of memory
    vb.memory = "8192"

    # Customize the amount of video memory
    vb.customize ["modifyvm", :id, "--vram", "128"]

    # Enable SSD in guest
    vb.customize ["storageattach", :id, "--storagectl",\
                  "SATA Controller", "--port", "0", \
                  "--device", "0", "--nonrotational", "on"]

    # Enable virtio for network cards
    vb.customize ["modifyvm", :id, "--nictype1", "virtio" ]
    vb.customize ["modifyvm", :id, "--nictype2", "virtio" ]
    vb.customize ["modifyvm", :id, "--nictype3", "virtio" ]

    # Enable bidirectional clipboard
    vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']
  end

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get install --yes python-apt
    sudo install -D -o root -g root -m 600 \
        {/home/vagrant,/root}/.ssh/authorized_keys
  SHELL

  # Run ansible
  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "setup.yml"
      ansible.ask_vault_pass = true
  end
end
