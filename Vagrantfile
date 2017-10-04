# Example load balancing
#
# Load balancer for two web servers
#
# NOTE: Make sure you have the ubuntu/trusty64 base box installed...
# vagrant box add trusty64 http://files.vagrantup.com/trusty64.box

nodes = [
  { :hostname => 'web1', :ip => '192.168.0.40', :box => 'ubuntu/trusty64' },
  { :hostname => 'web2', :ip => '192.168.0.41', :box => 'ubuntu/trusty64' },
  { :hostname => 'web3', :ip => '192.168.0.42', :box => 'ubuntu/trusty64' },
  { :hostname => 'lbserver',  :ip => '192.168.0.43', :box => 'ubuntu/trusty64', :ram => 512 }
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = "ubuntu/trusty64"
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]

      memory = node[:ram] ? node[:ram] : 256;
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "50",
          "--memory", memory.to_s,
        ]
      end
    end
  end
