# Please see the online documentation at
# https://docs.vagrantup.com.

# OPTIONS
require 'yaml'
options = YAML.load_file File.join(File.dirname(__FILE__), 'vagrant.yaml')
domains = [
    "yii2.dev",
    "backend.yii2.dev",
    "storage.yii2.dev"
]
packages = [
    "php5-cli",
    "php5-fpm",
    "php5-intl",
    "php5-gd",
    "php5-mysqlnd",
    "php5-curl",
    "php5-mcrypt",
    "php5-xdebug",
    "nginx",
    "mysql-server-5.6",
    "hhvm",
    "git"
]

Vagrant.configure(2) do |config|
  config.vm.post_up_message = "Done! Now you can access site at http://yii2.dev"
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = options['vm']['memory']
    vb.cpus = options['vm']['cpus']
    vb.name = options['vm']['name']
  end

  config.vm.define options['vm']['name'] {}

  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = domains[0]
  config.vm.network "private_network", ip: options['network']['ip']
  config.vm.synced_folder "./", "/var/www", id: "vagrant-root", :nfs => false, owner: "www-data", group: "www-data"

  config.vm.provision :hostmanager
  config.hostmanager.enabled            = true
  config.hostmanager.manage_host        = true
  config.hostmanager.ignore_private_ip  = false
  config.hostmanager.include_offline    = true
  config.hostmanager.aliases            = domains

  config.vm.provision "shell", path: "./vagrant.sh", args: [
    packages.join(" "),
    options['github']['token'],
    options['system']['swapsize'],
    options['system']['timezone']
  ]

  config.vm.provision "shell", inline: "service nginx restart", run: "always"
end