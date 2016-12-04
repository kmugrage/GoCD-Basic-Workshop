# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # The vbguest plugin often causes issues with the box for some reason. Should be
  # addressed instead of disabling it
  
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  config.vm.box = "2016-GoCD-Workshop.box"

  config.vm.network "forwarded_port", guest: 8153, host: 8153, autocorrect: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "2"
  end

end
