Snappy package
==========
This repository hosts snapcraft configuration file for building snappy package of [Nitrokey Application](https://www.nitrokey.com/).
Here are instructions about using snappy and snapcraft tools with it.
More details about snappy could be found at: [use](http://snapcraft.io/) [create](http://snapcraft.io/create/)

For users
=====
To install Nitrokey Application through snappy service please run command:
```
sudo snappy install nitrokey-app --devmode
```
Please notice `--devmode` switch. Without it application cannot communicate with USB devices.
After that application could be run with `nitrokey-app`.

For developers
========

To run application please use `nitrokey-app.dev` after standard installation.

To build package simply execute (please update the system beforehand, especially snappy family packages):

```
snapcraft update
snapcraft clean && snapcraft
```
Snappy will download latest sources from git repository and all dependences of application.
Then a snap package will be created in the root directory. It can be installed with:

```
sudo snap install nitrokey-app*snap --force-dangerous --devmode
```

It can be later sent to Ubuntu App store:
```
snapcraft login email@email.com # email from the Ubuntu App's account
snapcraft push nitrok*snap # note revision number
snapcraft release nitrokey-app <current revision>  stable
```
Please remember to set proper application version in snapcraft.yaml. Since Snappy is under heavy development it is possible some changes would have to be made in snapcraft.yaml.

In case snapd would lock and could not remove application (aka Snap uninstallation process fails):
[solution](http://askubuntu.com/questions/765778/snap-uninstallation-process-fails)
[src] (https://github.com/zyga/devtools/blob/master/reset-state)

Known issues:
=====

Current issues list could be found under [issues page](https://github.com/Nitrokey/nitrokey-app.snappy/issues).

Most important as of 20160715:
- A tray icon could not be shown (snappy platform issue) (update 20161129: should be fixed within a month)
- Could not install package without `--devmode`(no available interface for device talk)
- Not working with encrypted home: `failed to create user data directory. errmsg: Permission denied` -
    please check [solution](https://bugs.launchpad.net/ubuntu/+source/snapd/+bug/1592696/comments/8)
    and [solution 2](https://bugs.launchpad.net/ubuntu/+source/snapd/+bug/1592696/comments/7)

Warnings
=========
Some warnings are displayed during application execution:
```
XmbTextListToTextProperty result code -2
XmbTextListToTextProperty result code -2
XmbTextListToTextProperty result code -2
```
They are muted with standard `nitrokey-app` call. Cause is not yet known. Application seems to work properly nevertheless.
