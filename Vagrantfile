# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/debian-8.7"

  config.vm.network "forwarded_port", guest: 8123, host: 8123

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y python3-pip
    pip3 install homeassistant
    mkdir -p /root/.homeassistant/
    ln -s /vagrant/configuration.yaml /root/.homeassistant/configuration.yaml
    ln -s /vagrant/groups.yaml /root/.homeassistant/groups.yaml
    ln -s /vagrant/secrets.yaml /root/.homeassistant/secrets.yaml
  SHELL

  config.vm.provision "shell", run: "always", inline: <<-SHELL
    cd
    nohup hass 0<&- &>/dev/null &
  SHELL

end
