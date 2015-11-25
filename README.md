This repository contains complete vagrant configuration for [Yii2 advanced application](https://github.com/yiisoft/yii2-app-advanced).
Configuration based on configs from [trntv/yii2-starter-kit](https://github.com/trntv/yii2-starter-kit).

# Installation

1. Install [Virtualbox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/)
2. Copy all files from repository except .gitignore and README.md to your project root directory.
3. Create GitHub [personal API token](https://github.com/blog/1509-personal-api-tokens) and add it in `vagrant.yaml`
4. Run in your project root:
```
vagrant plugin install vagrant-hostmanager
vagrant plugin install vagrant-vbguest
vagrant up
```

That`s all. After provision application will be accessible on http://yii2.dev

Web server configured with three different web roots:
- yii2.dev => /path/to/app/frontend/web
- backend.yii2.dev => /path/to/app/backend/web
- storage.yii2.dev => /path/to/app/storage/web

You also can add vagrant files to .gitignore:
```
vagrant.sh
vagrant.yaml
Vagrantfile
vhost.conf
.vagrant/
```