# ANT dissector plugin for wireshark

## Quick Start

To automatically setup a VM with ubuntu and compile the correct version of wireshark and this plugin you can use the `Vagrantfile` provided in this repo.
Just install (Vagrant)[https://www.vagrantup.com/] on your Machine, clone this repo and execute `vagrant up` from inside the repo.

After the VM Setup finished reboot it with `vagrant reload` and login with
```
Username: vagrant
Password: vagrant
```

Then run Wireshark in a terminal with
```sh
$ ./wireshark/build/run/wireshark-gtk
```

## Compile + Install

Tested with Wireshark 2.2.6 on Ubuntu 16.04.

Install dependencies:
```sh
sudo apt-get install -y bison build-essential cmake flex git libglib2.0-dev libgtk-3-dev libpcap-dev
```

```sh
git clone https://github.com/wireshark/wireshark
cd wireshark
git checkout wireshark-2.2.6

cd plugins
git clone https://github.com/stloewen/wireshark-ant ant
cp Custom.m4.example Custom.m4
cp Custom.make.example Custom.make
sed -i 's/foo/ant/g' Custom.m4 Custom.make

cd ..
mkdir build
cd build
cmake .. -DCUSTOM_PLUGIN_SRC_DIR="plugins/ant"
make plugins
```

Now if you have Wireshark 2.2.6 already installed (from some repo etc.) you just need to copy the compiled plugin into the plugins directory (found by clicking on `Help -> About Wireshark`):
```sh
cp run/plugins/ant.so ~/.config/wireshark/plugins/
```

Otherwise continue to fully compile wireshark and run it from the build directory:
```sh
make all
cd run
./wireshark-gtk
```
