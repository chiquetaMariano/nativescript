# vagrant-nativescript
Vagrant box with NativeScript development environment up and running. Check it out on [Vagrant Cloud](https://app.vagrantup.com/marianoRafael/boxes/nativescript).

## Overview

Support for device debugging. It includes the basic tools to compile a NativeScript application (JDK, Android SDK, enviroment variables settings, Android Platform tools).

## Installation
In order to use this machine properly and allow debugging with your physical device, you should modify your `Vagrantfile` so your VirtualBox Machine detects your usb debugging port. Also, you'll need "Oracle VM VirtualBox Extension Pack" installed in order to use the USB port. Please check the [VirtualBox download section](https://www.virtualbox.org/wiki/Downloads) for more info.
You can also check out the `Vagrantfile` template included with this repository.

### Physical device setup

1. Plug in your device.
2. In your Vagrantfile you should enable usb ports in the following way:
```
  config.vm.provider "virtualbox" do |vb|
  
    .
    .
    .
    
    vb.customize ["modifyvm", :id, "--usb", "on"]
```
3. Save this file and run `vagrant up` and `vagrant ssh`. 

### Emulator (Android)

For the following steps you must have installed the `emulator` command line tool on your host machine (it is included with a clean installation of Android Studio). For more info [checkout here](https://developer.android.com/studio/run/emulator-commandline). Open a terminal in your host machine and follow 
the next steps:

1. List your emulators through CLI by running `emulator -list-avds`. The emulator command line tool is generally located at `ANDROID_HOME/emulator`.
2. Choose one emulator from the list and run `emulator @<your_emulator>`.
3. Now, in your vagrant machine, execute the following commands: `adb connect 10.0.2.2:5555`. The IP address belongs to your host machine as seen from the vagrant
machine (`10.0.2.2` by default) and the port number is the adb port of the emulator (5555 is generally assigned to the first emulator you open). [More info](https://developer.android.com/studio/command-line/adb#move).

### Development workflow

Now you can put your project files in your shared folder and simply run `ns run android` in that folder.
However, take into account that performance for compilation operations in shared folders is penalized, so you should enable NFS filesystem type in your Vagrantfile. If you're using a Windows host you can use WinNFSd plugin to enable NFS.

In your nativescript app project, you should enable webpack polling to detect changes in your project files. You can achieve this by adding this lines to webpack.config.js:
```
module.exports = (env) => {
      .
      .
      .
	webpack.mergeWebpack(env => {
		return {
		    watchOptions: {
				poll: true,
			  },
			}
		});
      .
      .
      .
	return webpack.resolveConfig();
};

```
