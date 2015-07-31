# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network :private_network, ip: "192.168.33.10"

  # Local Machine Hosts
  #
  # If the Vagrant plugin hostsupdater (https://github.com/cogitatio/vagrant-hostsupdater) is
  # installed, the following will automatically configure your local machine's hosts file to
  # be aware of the domains specified below. Watch the provisioning script as you may need to
  # enter a password for Vagrant to access your hosts file.
  if defined?(VagrantPlugins::HostsUpdater)
    config.hostsupdater.aliases = "local.tryghost.org"
    config.hostsupdater.remove_on_suspend = true
  end

  config.vm.synced_folder "Ghost/", "/home/vagrant/code/Ghost"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file  = "base.pp"
    puppet.module_path = "modules"
  end
end
