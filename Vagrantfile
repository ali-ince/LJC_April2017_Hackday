$script = <<SCRIPT
sudo apt-get update
sudo systemctl disable apt-daily.service
sudo systemctl disable apt-daily.timer
sudo apt-get install -y lubuntu-desktop virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11
mkdir /home/vagrant/Desktop
SCRIPT

$jdk8script = <<SCRIPT
echo "Installing JDK 8"
wget -nv --header "Cookie: oraclelicense=accept-securebackup-cookie" -O /tmp/jdk-8u131-linux-x64.tar.gz http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz
sudo tar -zxf /tmp/jdk-8u131-linux-x64.tar.gz -C /opt
SCRIPT

$jdk9script = <<SCRIPT
echo "Installing JDK 9..."
wget -nv -O /tmp/jdk-9-ea+165_linux-x64_bin.tar.gz http://download.java.net/java/jdk9/archive/165/binaries/jdk-9-ea+165_linux-x64_bin.tar.gz
sudo tar -zxf /tmp/jdk-9-ea+165_linux-x64_bin.tar.gz -C /opt
sudo awk -e 'BEGIN { print "export JAVA_HOME=/opt/jdk-9\\nPATH=$PATH:$JAVA_HOME/bin" }' > /etc/profile.d/jdk.sh
rm -rf /tmp/jdk-9-ea+165_linux-x64_bin.tar.gz
SCRIPT

$ideascript = <<SCRIPT
echo "Installing IntelliJ 2017.1..."
wget -nv -O /tmp/ideaIC-2017.1.1.tar.gz https://download.jetbrains.com/idea/ideaIC-2017.1.1.tar.gz
sudo tar -zxf /tmp/ideaIC-2017.1.1.tar.gz -C /opt
sudo awk -e 'BEGIN { print "IDEA_HOME=/opt/idea-IC-171.4073.35\\nPATH=$PATH:$IDEA_HOME/bin" }' > /etc/profile.d/idea.sh
sudo awk -e 'BEGIN { print "[Desktop Entry]\\nType=Application\\nExec=/opt/idea-IC-171.4073.35/bin/idea.sh\\nGenericName=IntelliJ Idea\\nIcon=/opt/idea-IC-171.4073.35/bin/idea.png" }' > /home/vagrant/Desktop/Idea
rm -rf /tmp/ideaIC-2017.1.1-no-jdk.tar.gz
SCRIPT

$eclipsescript = <<SCRIPT
echo "Installing Eclipse Neon..."
wget -nv -O /tmp/eclipse-jee-neon-3-linux-gtk-x86_64.tar.gz http://ftp-stud.fht-esslingen.de/pub/Mirrors/eclipse/technology/epp/downloads/release/neon/3/eclipse-jee-neon-3-linux-gtk-x86_64.tar.gz
sudo tar -zxf /tmp/eclipse-jee-neon-3-linux-gtk-x86_64.tar.gz -C /opt
sudo ln -s /opt/jdk1.8.0_131/jre /opt/eclipse/jre
sudo awk -e 'BEGIN { print "ECLIPSE_HOME=/opt/eclipse\\nPATH=$PATH:$ECLIPSE_HOME" }' > /etc/profile.d/eclipse.sh
sudo awk -e 'BEGIN { print "[Desktop Entry]\\nType=Application\\nExec=/opt/eclipse/eclipse\\nGenericName=Eclipse\\nIcon=/opt/eclipse/icon.xpm" }' > /home/vagrant/Desktop/Eclipse
rm -rf /tmp/eclipse-jee-neon-3-linux-gtk-x86_64.tar.gz
SCRIPT

$nbscript = <<SCRIPT
echo "Installing Netbeans 8.2..."
wget -nv -O /tmp/netbeans-8.2-201609300101-javaee.zip http://download.netbeans.org/netbeans/8.2/final/zip/netbeans-8.2-201609300101-javaee.zip
sudo unzip -q /tmp/netbeans-8.2-201609300101-javaee.zip -d /opt
sudo sed -i -e 's/#netbeans_jdkhome="\\/path\\/to\\/jdk"/netbeans_jdkhome="\\/opt\\/jdk1.8.0_131"/g' /opt/netbeans/etc/netbeans.conf
sudo awk -e 'BEGIN { print "NB_HOME=/opt/netbeans\\nPATH=$PATH:$NB_HOME/bin" }' > /etc/profile.d/nb.sh
sudo awk -e 'BEGIN { print "[Desktop Entry]\\nType=Application\\nExec=/opt/netbeans/bin/netbeans\\nGenericName=Netbeans\\nIcon=/opt/netbeans/nb/netbeans.png" }' > /home/vagrant/Desktop/Netbeans
rm -rf /tmp/netbeans-8.2-201609300101-javaee.zip
SCRIPT

VAGRANTFILE_API_VERSION = "2"

require './vagrant-provision-reboot-plugin'

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.10"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "Project", "/home/vagrant/Project"

  config.vm.provider "virtualbox" do |v|
    v.name = "22 April 2017 - Hackday"
    v.memory = 8192 
    v.cpus = 4
    v.gui = true
  end

  config.vm.provision "shell", inline: $script
  config.vm.provision "shell", inline: $jdk8script
  config.vm.provision "shell", inline: $jdk9script
  config.vm.provision "shell", inline: $ideascript
  config.vm.provision "shell", inline: $eclipsescript
  config.vm.provision "shell", inline: $nbscript
  config.vm.provision :unix_reboot
end
