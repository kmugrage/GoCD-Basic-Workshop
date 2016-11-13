
GoCD Workshop
----

This repository contains the files required to run my GoCD workshop. The workshop is designed to introduce continuous delivery concepts using GoCD. 

####Contents
* Vagrantfile - This references a machine on atlas.hashicorp.com.
	* The virtual machine *will* change as I do more workshops and GoCD has new releases.
	* The virtual machine has all of the software needed for the workshop
		* git repositories
		* Docker beta elastic agent plugin
		* GoCD yaml configuration plugin
	* The instructions linked below go through the creation of several dependent pipelines
	* The "finished" yaml is also in .finished-yaml if you need to cheat

####To run the virtual machine

* Fork this repository (if you clone from here there's a high chance something will change that you may not expect)
* Bring up a command prompt 
* Type 'vagrant up' to start the machine
	* Note: This could take a long time the first time, depending on your available bandwidth. The virtual machine is 1.2GB. You do _not_ want to do this on a plane

####Clone workshop source code out of git server on VM

## On this branch we don't clone the code out of the VM. This is to lower the system requirements when distributed on USB Drive

Workshop instructions at https://github.com/kmugrage/GoCD-Basic-Workshop/blob/master/WorkshopInstructions.md

