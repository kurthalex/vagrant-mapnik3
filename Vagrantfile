# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "debian/jessie64"
  config.vm.hostname = "myjessie"
  config.vm.box_check_update = "true"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "shared", "/home/vagrant/shared"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "mapnik3-dev"
    vb.memory = "6144"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get -y install git vim clang-3.4 auto-apt libcairomm-1.0-dev python-setuptools python-dev libxslt1-dev
    sudo easy_install pip
    sudo su -c "echo 'deb http://ftp.debian.org/debian jessie/main /' >> /etc/apt/sources.list" # for auto-apt
    sudo auto-apt update
    git clone https://github.com/mapnik/mapnik.git
    cd mapnik
    git checkout v3.0.9
    sudo auto-apt -y run ./configure
    make CC=clang CCX=clang++
    make install
    sudo apt-get install libxslt1-dev
    sudo pip install mapnik
    cd ..
    git clone https://github.com/Mappy/pycnik.git
    cd pycnik
    python setup.py install
    cd ..

  SHELL
end


