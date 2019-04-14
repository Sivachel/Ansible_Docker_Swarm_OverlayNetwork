required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
   unless Vagrant.has_plugin? (plugin)
     #Uses vagrant plugin manager to install plugin, which will automatically refresh plugin list
     puts "Installing vagrant plugin #{plugin}"
     Vagrant::Plugin::Manager.instance.install_plugin plugin
     puts "Installed vagrant plugin #{plugin}"
   end
end

Vagrant.configure(2) do |config|
  config.vm.define "manager" do |manager|
    manager.vm.box = "ubuntu/xenial64"
    manager.vm.network "private_network", ip: "192.168.10.100"
    manager.hostsupdater.aliases = ["manager.local"]
    manager.vm.provision "ansible_local" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "manager_provisioning.yml"
      ansible.become = true
    end
  end

  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/xenial64"
    db.vm.network "private_network", ip: "192.168.10.120"
    db.hostsupdater.aliases = ["db.local"]
    db.vm.provision "ansible_local" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "db_provisioning.yml"
      ansible.become = true
    end
  end

  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.130"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.provision "ansible_local" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "app_provisioning.yml"
      ansible.become = true
    end
  end
end
