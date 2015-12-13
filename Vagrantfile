# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network "private_network", ip: "192.168.50.4"
  config.vm.network "public_network"
  config.vm.hostname = "elastic.try"

  config.vm.synced_folder '.', '/var/www/elastic', nfs: true
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |v|
    v.gui = false

    v.cpus = "2"
    v.name = "ubuntu_elastic.box"
    v.customize ["modifyvm", :id, "--memory",               "2048"]
    v.customize ["modifyvm", :id, "--cpuexecutioncap",      "95"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1",  "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1",         "on"]
  end

  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  config.vm.provision :shell, path: "vagrant/php.sh"
  config.vm.provision :shell, path: "vagrant/mysql.sh"

  config.vm.provision :shell, :inline => <<-EOT
       echo 'LC_ALL="en_US.UTF-8"'  >  /etc/default/locale
  EOT
end
