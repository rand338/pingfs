# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 4
    vb.memory = "4096"
    vb.linked_clone = true
    vb.name = "pingfs"
  end

  pingfs_root_dir = File.join("/opt", "pingfs")

  config.vm.provision "shell", name: "Update-Package-List", inline: <<-SHELL
    apt-get update
    apt-get install -y libfuse-dev pkg-config
  SHELL

  config.vm.provision "shell", name: "pingfs-setup", inline: <<-SHELL
    mkdir -p #{pingfs_root_dir}
    if [ ! -L /home/vagrant/pingfs ]; then
        ln -s #{pingfs_root_dir} /home/vagrant
    fi 
    chown -R vagrant: #{pingfs_root_dir}
  SHELL


  if File.directory?(File.absolute_path('../pingfs'))
    config.vm.synced_folder File.absolute_path('../pingfs'), pingfs_root_dir
  end


end
