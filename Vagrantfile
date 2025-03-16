# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

vms = {
  'wildfly-domain' => {'memory' => '2048', 'cpus' => 2, 'ip' => '100', 'box' => 'rocky-linux-9-desktop/rocky-linux-9-desktop', 'provision' => 'provision/ansible/wildfly-domain.yaml'},
  'wildfly-controller1' => {'memory' => '1536', 'cpus' => 2, 'ip' => '101', 'box' => 'rocky-linux9-vagrant/rocky-linux9-vagrant', 'provision' => 'provision/ansible/wildfly-controller1.yaml'},
  'wildfly-controller2' => {'memory' => '1536', 'cpus' => 2, 'ip' => '102', 'box' => 'rocky-linux9-vagrant/rocky-linux9-vagrant', 'provision' => 'provision/ansible/wildfly-controller2.yaml'},
  'devops-node' => {'memory' => '2048', 'cpus' => 2, 'ip' => '103', 'box' => 'rocky-linux9-vagrant/rocky-linux9-vagrant', 'provision' => 'provision/ansible/devops-node.yaml'},
  'monitoring-node' => {'memory' => '2048', 'cpus' => 2, 'ip' => '104', 'box' => 'rocky-linux9-vagrant/rocky-linux9-vagrant', 'provision' => 'provision/ansible/monitoring-node.yaml'}
}

Vagrant.configure('2') do |config|
  config.vm.box_check_update = false
  
  vms.each do |name, conf|
    config.vm.define "#{name}" do |k|
      k.vm.box = "#{conf['box']}"
      k.vm.hostname = "#{name}"
      k.vm.network 'private_network', ip: "172.16.0.#{conf['ip']}"
      
      k.vm.provider 'virtualbox' do |vb|
        vb.name = "#{name}"
        vb.memory = conf['memory']
        vb.cpus = conf['cpus']
      end
      k.vm.provision 'ansible_local' do |ansible|
        ansible.install = false
        ansible.playbook = "#{conf['provision']}"
        ansible.compatibility_mode = '2.0'
      end
    end
  end
end

