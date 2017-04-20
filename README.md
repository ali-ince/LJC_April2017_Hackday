# LJC_April2017_Hackday

Vagrant VM Preparation (VirtualBox) for Prerequisites of LJC April 2017 Hackday

As per the preparation guidelines sent by Mani, I have setup a Vagrant configuration based on Ubuntu Linux which simply creates a VirtualBox machine with GUI support and installs / configures the following components (all installed components are added to PATH during the provisioning phase);

1. Ubuntu 16.10 based on bento/ubuntu-16.10 box.
2. Installs lubuntu-desktop and its dependencies (includes firefox).
3. Installs JDK 9 Early Access (build 165) (invoke java from command line). 
4. Installs IntelliJ IDEA Community (2017.1) (invoke idea.sh from command line).
5. Installs Eclipse IDE for Java EE Developers (Neon) (invoke eclipse from command line).
6. Installs Netbeans Java EE bundle (8.2) (invoke netbeans from command line).

Feel free to modify any settings or provisioning steps for your environment.

Note: Thanks to @exratione for his Vagrant Reboot Provisioner plugin shared through https://www.exratione.com/2014/06/how-to-reboot-a-vagrant-guest-vm-during-provisioning/.
