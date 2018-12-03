Vagrant.configure("2") do |config|

  config.vm.define 'user' do |config|
  config.vm.provider :digital_ocean do |provider, override|
   override.ssh.private_key_path = '/root/.ssh/id_rsa'
   override.vm.box = 'digital_ocean'
   override.vm.box_url = "https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box"
   provider.token = ''
   provider.image = 'ubuntu-16-04-x64'
   provider.region = 'fra1'
   provider.size = '512mb'
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update > /dev/null
    test -x /usr/bin/python || apt-get -y install python2.7-minimal
    update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
  SHELL

  config.vm.provision :ansible do |ansible|
  ansible.playbook = "ansible-app/Deploy_goapp.yml"
  end
end
