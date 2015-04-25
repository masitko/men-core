# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "trusty64"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
#  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/20141125/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.

    config.vm.network :forwarded_port, guest: 80,   host: 8018, auto_correct: true
    config.vm.network :forwarded_port, guest: 8019, host: 8019, auto_correct: true


  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
    config.vm.network :private_network, ip: "192.168.80.18"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
    config.vm.synced_folder "code/quiz", "/var/www/quiz", type: "nfs"
#    config.vm.synced_folder "code/node", "/var/www/node", type: "nfs"
#    config.vm.synced_folder "code/resident", "/var/www/resident", type: "nfs"
#    config.vm.synced_folder "code/main", "/var/www/main", type: "nfs"
#    config.vm.provision :shell, :path => "messages.sh"

config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "puppet/manifests"
    puppet.module_path = "puppet/modules"
    puppet.options = "--verbose --debug --fileserverconfig=/vagrant/puppet/files/fileserver.conf"
end
  config.vm.provision :shell, :path => "db.sh"

 # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider :virtualbox do |virtualbox|
     virtualbox.customize ["modifyvm", :id, "--name", "quiz"]
     virtualbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
     virtualbox.customize ["modifyvm", :id, "--memory", "1024"]
     virtualbox.customize ["modifyvm", :id, "--cpus", 1]

#     virtualbox.customize ["setextradata", :id, "--VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

 
  
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest in
  # the file base.pp in the manifests_path directory.
  #
  # An example Puppet manifest to provision the message of the day:
  #
  # # group { "puppet":
  # #   ensure => "present",
  # # }
  # #
  # # File { owner => 0, group => 0, mode => 0644 }
  # #
  # # file { '/etc/motd':
  # #   content => "Welcome to your Vagrant-built virtual machine!
  # #               Managed by Puppet.\n"
  # # }
  #
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "manifests"
  #   puppet.manifest_file  = "site.pp"
  # end

end
