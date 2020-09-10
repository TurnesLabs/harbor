Vagrant.configure("2") do |config|
  config.vagrant.plugins = ["vagrant-env"]  # make sure vagrant have the plugin
  config.env.enable



  config.vm.define ENV['HARBOR_HOSTNAME'] do |harbor|
    harbor.vm.box = ENV['HARBOR_OS']
    harbor.vm.hostname = ENV['HARBOR_HOSTNAME']
    harbor.vm.network "private_network", ip: ENV['HARBOR_IP']

    config.vm.provider "virtualbox" do |v|
      v.name = ENV['HARBOR_HOSTNAME']
      v.cpus= ENV['HARBOR_CPU']
      v.memory = ENV['HARBOR_MEMORY']
    end
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "playbooks/00-check.yml"
    ansible.become = true
    ansible.groups = {
        "registry_nodes" => [ENV['HARBOR_HOSTNAME']]
    }
    ansible.extra_vars = {}
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "playbooks/01-prerequisites.yml"
    ansible.become = true
    ansible.groups = {
        "registry_nodes" => [ENV['HARBOR_HOSTNAME']]
    }
    ansible.extra_vars = {}
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "playbooks/02-install-harbor.yml"
    ansible.become = true
    ansible.groups = {
        "registry_nodes" => [ENV['HARBOR_HOSTNAME']]
    }
    ansible.extra_vars = {
      "harbor_ip" => ENV['HARBOR_IP'],
      "harbor_admin_password" => ENV['HARBOR_ADMIN_PASSWORD'],
    }
  end
end
