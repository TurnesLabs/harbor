Vagrant.configure("2") do |config|
  config.vagrant.plugins = ["vagrant-env"]  # make sure vagrant have the plugin
  config.env.enable



  config.vm.define "harbor" do |harbor|
    harbor.vm.box = ENV['HARBOR_OS']
    harbor.vm.hostname = ENV['HARBOR_HOSTNAME']
    harbor.vm.network "private_network", ip: ENV['HARBOR_IP']

    config.vm.provider "virtualbox" do |v|
      v.name = ENV['HARBOR_HOSTNAME']
      v.cpus= ENV['HARBOR_CPU']
      v.memory = ENV['HARBOR_MEMORY']
    end
  end
end
