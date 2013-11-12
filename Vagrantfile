# -*- mode: ruby -*-
# vi: set ft=ruby :

#http://misheska.com/blog/2013/06/16/getting-started-writing-chef-cookbooks-the-berkshelf-way/
#Install following and do VagrantUp
#http://www.vagrantup.com/
#https://www.virtualbox.org/wiki/Downloads
#gem install berkshelf --no-ri --no-rdoc
#vagrant plugin install vagrant-berkshelf
#vagrant plugin install vagrant-omnibus

Vagrant.configure("2") do |config|
 config.vm.box = "ubuntu-13.04-mini-i386.box"
 config.vm.box_url = "https://dl.dropboxusercontent.com/u/4387941/vagrant-boxes/ubuntu-13.04-mini-i386.box"
 config.vm.network :forwarded_port, guest: 80, host: 9881
 config.vm.network :private_network, ip: "192.168.33.10"
 # config.vm.network :public_network
 config.vm.synced_folder ".", "/source"
 config.vm.synced_folder "../", "/projects"
 config.vm.provider :virtualbox do |vb|
  vb.gui = false
  vb.customize ["modifyvm", :id, "--memory", "1024"]
 end
 config.vm.provision :shell, :inline => <<-PROVISION
    cd /source
    gem install berkshelf
    berks install --path /source/.vendor/cookbooks/
    chef-solo -c /source/solo.rb -j /source/run_list.json
    cd /projects/billu
    bundle install
 PROVISION
end
