# vagrant-ubuntu-20.04-gdal

## Create Box

Create vagrant vm from `Vagrantfile`

```
vagrant up
```

Make the Box as Small as possible

```
vagrant ssh
sudo apt-get clean
sudo dd if=/dev/zero of=/EMPTY bs=1M
sudo rm -f /EMPTY
cat /dev/null > ~/.bash_history && history -c && exit
```

Repackage the VM into a New Vagrant Box

```
vagrant package --output mynew.box
```

Upload box / create new version etc. in browser: https://app.vagrantup.com/boxes/new / https://app.vagrantup.com/sogis/boxes/ubuntu-gdal-3.0/versions/new 

**Do not forget to release the new version.**

## Use Box

Create Vagrantfile:
```
vagrant init sogis/ubuntu-gdal-3.0
```

Adjust Vagrantfile:
```
config.vm.network "forwarded_port", guest: 22, host: 2020, id: 'ssh'
config.ssh.forward_agent = true
config.ssh.forward_x11 = true
```

and if you want to run some heavier tasks (the bigger the better):

```
vb.memory = "8192"
vb.cpus = 2
```

Start / create vm:
```
vagrant up
```

Login with `vagrant ssh`.
