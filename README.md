
GoCD Workshop
----

To run this workshop...

1. Clone this repository
2. Bring up a command prompt 
3. Type 'vagrant up' to start the machine
	* Note: This could take a long time the first time, depending on your available bandwidth. The virtual machine is 1.2GB. You do _not_ want to do this on a plane
4. Modify your SSH configuration to use the Vagrant key. (Note, this step is optional. If you prefer, you can use the built in 'vagrant ssh' to access the box as the vagrant user.)
	* Type 'vagrant ssh-config' - This will give you output that looks something like:
	'''
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/kenmugrage/.vagrant.d/boxes/gocd-VAGRANTSLASH-2016-workshop/1.0/virtualbox/vagrant_private_key
  IdentitiesOnly yes
  LogLevel FATAL
  '''