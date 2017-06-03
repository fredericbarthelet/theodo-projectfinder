PROJECT_NAME = 'theodo-projectfinder'

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = PROJECT_NAME
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network :private_network, ip: "199.199.199.12"
  config.vm.synced_folder ".", "/var/www/projectfinder/current", type: "nfs"
  config.vm.provider 'virtualbox' do |v|
    v.customize ['modifyvm', :id, '--cpuexecutioncap', 100]
    v.customize ['modifyvm', :id, '--memory', 2048]
    v.customize ['modifyvm', :id, '--cpus', 2]
    v.name = PROJECT_NAME
  end
  config.ssh.forward_agent = true

  # Ansible see https://docs.vagrantup.com/v2/provisioning/ansible.html
  config.vm.provision "ansible" do |ansible|
    ansible.sudo = true
    ansible.playbook = "provisioning/playbook.yml"
    ansible.limit = 'vagrant'
    ansible.inventory_path = "provisioning/hosts/vagrant"
    ansible.verbose = "v" #Use vvvv to get more log
  end
end
