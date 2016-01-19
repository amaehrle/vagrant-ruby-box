# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.network 'forwarded_port', guest: 5000, host: 5000
  config.vm.network 'forwarded_port', guest: 5100, host: 5100
  config.vm.network 'forwarded_port', guest: 9292, host: 9292

  config.vm.provision 'file', source: '~/.gitconfig', destination: '.gitconfig'
  config.vm.synced_folder './workspace', '/home/vagrant/workspace'

  # config.vm.provision :shell, inline: [
  #   'apt-add-repository ppa:brightbox/ruby-ng',
  #   'apt-get -y -q update',
  #   'apt-get -y -q upgrade',
  #   'apt-get -y -q install build-essential zlib1g-dev libssl-dev libreadline6-dev libyaml-dev', 
  #   'apt-get -y -q install ruby2.2-dev libsqlite3-dev',
  #   'apt-get -y -q install ruby2.2',

  #   'wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh',

  #   'apt-get -y -q install libpq-dev postgresql postgresql-contrib',
  #   'echo PATH="/usr/lib/postgresql/9.3/bin:$PATH" >> /home/vagrant/.bashrc',

  #   ## project depended: (need to prove it works)
  #   'git clone https://github.com/elasticdog/transcrypt.git',
  #   'cd transcrypt/',
  #   'ln -s ${PWD}/transcrypt /usr/local/bin/transcrypt',
  #   'cd /home/vagrant'

  #   # 'cd /home/vagrant/workspace/reColl-android-server',
  #   # 'gem install bundler',
  #   # 'bundle install',
  #   # 'postgres -D /usr/local/var/postgres',
  #   # 'bundle exec rake db:create && db:init'

  # ].join(' && ')

  config.vm.provision :ansible do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', '2048']
    vb.customize ['modifyvm', :id, '--cpus', '2']
  end
end

