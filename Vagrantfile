# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  else
    puts "_Info_: Plugin '''vagrant-cachier''' is not installed."
    puts "To install, run: vagrant plugin install vagrant-cachier"
  end

  unless Vagrant.has_plugin?("vagrant-rsync-back")
    puts "_Info_: Plugin '''vagrant-rsync-back''' is not installed."
    puts "To install, run: vagrant plugin install vagrant-rsync-back"
  end

  config.vm.box = "ubuntu/trusty32"

  config.vm.hostname = "vm"
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
  end

  config.vm.network "forwarded_port", guest: 8042, host: 8042,
    auto_correct: true

  config.vm.synced_folder ".", "/vagrant", type: "rsync",
    rsync__auto: true

  config.vm.provision "shell" do |s|
    s.inline = <<SCRIPT
echo "*************************"
echo "Updating system packages"
echo "*************************"

sudo apt-get -y update
sudo apt-get -y upgrade
sudo locale-gen pt_BR.UTF-8

echo "******************************"
echo "Installing supporting packages"
echo "******************************"

sudo apt-get -y install build-essential wget curl git vim
sudo apt-get -y install libcurl4-gnutls-dev libreadline-dev libxml2-dev libxslt1-dev re2c libpng-dev libjpeg-dev m4 lcov

echo "*********************"
echo "Installing oh-my-zsh"
echo "*********************"

sudo apt-get -y install zsh
sudo su - vagrant -c 'curl -L http://install.ohmyz.sh | zsh'
sudo sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="agnoster"/' /home/vagrant/.zshrc
sudo sed -i 's=:/bin:=:/bin:/sbin:/usr/sbin:=' /home/vagrant/.zshrc
chsh vagrant -s $(which zsh);

echo "****************************"
echo "Installing php5 dev packages"
echo "****************************"

sudo apt-get -y install php5-dev php-pear

echo "*********************************"
echo "Installing bison required version"
echo "*********************************"

wget http://launchpadlibrarian.net/140087287/libbison-dev_2.7.1.dfsg-1_i386.deb
wget http://launchpadlibrarian.net/140087286/bison_2.7.1.dfsg-1_i386.deb
sudo dpkg -i libbison-dev_2.7.1.dfsg-1_i386.deb
sudo dpkg -i bison_2.7.1.dfsg-1_i386.deb
rm -rf libbison-dev_2.7.1.dfsg-1_i386.deb
rm -rf bison_2.7.1.dfsg-1_i386.deb

SCRIPT
  end

end
