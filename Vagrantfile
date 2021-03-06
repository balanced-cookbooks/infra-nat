# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure '2' do |config|

  def apply_test_vm_defaults(config)
    config.vm.box     = 'precise64'
    config.vm.box_url = 'https://s3.amazonaws.com/gsc-vagrant-boxes/ubuntu-12.04-omnibus-chef.box'
    config.vm.network :private_network, ip: '192.168.33.11'
  end

  project_name = File.basename(Dir.getwd)

  config.vm.synced_folder '.', "/home/vagrant/#{project_name}"

  config.vm.define project_name do |box|
    apply_test_vm_defaults box

    config.vm.provision :ansible do |ansible|
      ansible.playbook       = './tests/vagrant.yml'
      ansible.inventory_path = './tests/vagrant-inventory'
      ansible.extra_vars     = {
          ansible_ssh_user: 'vagrant',
          sudo: true
      }
    end
  end

  config.vm.define 'nat' do |box|
    apply_test_vm_defaults box

    config.vm.provision :ansible do |ansible|
      ansible.playbook       = './vagrant-nat.yml'
      ansible.inventory_path = './tests/vagrant-inventory'
      ansible.extra_vars     = {
          ansible_ssh_user: 'vagrant',
          sudo: true
      }
    end

  end

end
