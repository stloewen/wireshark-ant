# ANT dissector plugin for wireshark

## Compile + Install

Tested with Wireshark 2.2.6 on Ubuntu 16.04.

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

cp run/plugins/ant.so ~/.config/wireshark/plugins/
```
