# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  config.vm.define = "testserver"

  config.vm.network "forwarded_port", id: 'ssh', guest: 22, host: 2202, host_ip: "127.0.0.1", auto_correct: false  
  config.vm.network "forwarded_port", id: 'http', guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", id: 'https', guest: 443, host: 8443, host_ip: "127.0.0.1"
  
  # Запретить обновление дополнений гостевой системы
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  config.vm.provider "virtualbox" do |virtualbox|
    # Указываем количество ОЗУ и ядер процессора
    virtualbox.name = "node1"
    virtualbox.memory = "1024"
    virtualbox.cpus = "1"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.version = "2.10.8"
    ansible.playbook = "webservers.yml"
  end

end
