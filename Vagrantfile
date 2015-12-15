# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'
  config.vm.synced_folder './workspace', '/home/vagrant/workspace'
  config.vm.network 'forwarded_port', guest: 5000, host: 5000
  config.vm.network 'forwarded_port', guest: 5100, host: 5100

  config.ssh.forward_agent = true
  config.ssh.private_key_path = "~/.ssh/id_rsa"
  config.vm.provision 'file', source: '~/.gitconfig', destination: '.gitconfig'

  config.vm.provision :shell, inline: [
    'apt-add-repository ppa:brightbox/ruby-ng',
    'apt-get -y -q update',
    'apt-get -y -q upgrade',
    'apt-get -y -q install build-essential zlib1g-dev libssl-dev libreadline6-dev libyaml-dev',
    'apt-get -y -q install ruby2.2',
    'wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh',
    'sudo gem install bundler'
  ].join(' && ')

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', '2048']
    vb.customize ['modifyvm', :id, '--cpus', '2']
  end
end

