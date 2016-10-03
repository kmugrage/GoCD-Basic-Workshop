# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vbguest.auto_update = false

  config.vm.box = "gocd/2016-workshop"

  config.vm.network "forwarded_port", guest: 8153, host: 8153, autocorrect: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "2"
  end

end
