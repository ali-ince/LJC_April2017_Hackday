# LJC_April2017_Hackday

Vagrant VM Preparation (VirtualBox) for Prerequisites of LJC April 2017 Hackday

As per the preparation guidelines sent by Mani, I have setup a Vagrant configuration based on Ubuntu Linux which simply creates a VirtualBox machine with GUI support and installs / configures the following components (all installed components are added to PATH during the provisioning phase);

1. Ubuntu 16.10 based on bento/ubuntu-16.10 box.
2. Installs lubuntu-desktop and its dependencies (includes firefox).
3. Installs JDK 9 Early Access (build 165) (invoke java from command line). 
4. Installs IntelliJ IDEA Community (2017.1) (invoke idea.sh from command line).
5. Installs Eclipse IDE for Java EE Developers (Neon) (invoke eclipse from command line).
6. Installs Netbeans Java EE bundle (8.2) (invoke netbeans from command line).
7. Creates a synced folder named project which is usable in the VM and syncs to your local fs.

Feel free to modify any settings or provisioning steps for your environment.

In order to use;

1. Install Vagrant from https://www.vagrantup.com/downloads.html for your platform (Please note that the Vagrantfile I've created is crafted using VirtualBox as the provider).
2. Clone this repository.
3. Go to the local directory and issue "vagrant up". This will install and configure all dependencies and restart your VM (may take a while). When the command finishes you're ready to go!
4. In order to stop or suspend the VM, issue "vagrant halt" or "vagrant suspend" respectively.
5. When you do not need the VM anymore, you can delete all resources allocated by issuing "vagrant destroy". As long as you use the synced folder in the VM, you will not lose anything - which I like the most while using Vagrant.

Note: Thanks to @exratione for his Vagrant Reboot Provisioner plugin shared through https://www.exratione.com/2014/06/how-to-reboot-a-vagrant-guest-vm-during-provisioning/.
