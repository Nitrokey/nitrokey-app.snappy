Snappy package
==========
This repository hosts snapcraft configuration file for building snappy package of [Nitrokey Application](https://www.nitrokey.com/).
Here are instructions about using snappy and snapcraft tools with it.
More details about snappy could be found at: [use](http://snapcraft.io/) [create](http://snapcraft.io/create/)

For users
=====
To install Nitrokey Application through snappy service please run command:
```
sudo snap install nitrokey-app --devmode
```
Please notice `--devmode` switch. Without it application cannot communicate with USB devices.
After that application could be run with `nitrokey-app`.
If you wish to use Beta or Nightly versions please add `--beta` or `--edge` switch respectively.
In case you have already installed application from other source and it covers Snap path, you can use Snap directly to run the application:
```
snap run nitrokey-app 
```

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
Use `edge` for test builds and `beta` for builds destined to be tested by users.
Please remember to set proper application version in snapcraft.yaml. Since Snappy is under heavy development it is possible some changes would have to be made in snapcraft.yaml.

In case snapd would lock and could not remove application (aka Snap uninstallation process fails):
[solution](http://askubuntu.com/questions/765778/snap-uninstallation-process-fails)
[src] (https://github.com/zyga/devtools/blob/master/reset-state)

Known issues:
=====

Current issues list could be found under [issues page](https://github.com/Nitrokey/nitrokey-app.snappy/issues).

Most important as of 2018-04-11:
- Could not install package without `--devmode`

Warnings
=========
A warning is displayed during application execution:
```
Qt: Session management error: None of the authentication protocols specified are supported
```
Cause is not yet known. Application seems to work properly nevertheless.
