
GoCD Workshop
----

####To run the virtual machine

* Clone this repository
* Bring up a command prompt 
* Type 'vagrant up' to start the machine
	* Note: This could take a long time the first time, depending on your available bandwidth. The virtual machine is 1.2GB. You do _not_ want to do this on a plane

####Clone workshop source code out of git server on VM

Next we need to modify your SSH configuration to use the Vagrant key. (Note, this step is optional. The point is to allow you to clone the git repos in the virtual machine with your own user so that you can use your own text editors, git clients or other tools. If you prefer, you can use the built in 'vagrant ssh' to access the box as the vagrant user and use the Linux command line tools.)

* Type 'vagrant ssh-config' - This will give you output that looks something like:

```markdown
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
```

* Copy the line that begins with **IdentityFile**
* On your system, edit ~/.ssh/config and add the following section:

```markdown
Host workshop
    HostName localhost
    Port 2222
    IdentityFile /Users/kenmugrage/.vagrant.d/boxes/gocd-VAGRANTSLASH-2016-workshop/1.0/virtualbox/vagrant_private_key
    User vagrant
```

* Type 'git clone ssh://vagrant@workshop/gitrepo/application.git'
* Type 'git clone ssh://vagrant@workshop/gitrepo/gocd-configuration.git'

Workshop instructions at https://github.com/kmugrage/GoCD-Basic-Workshop/blob/master/WorkshopInstructions.md

