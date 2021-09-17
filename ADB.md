> Android Debug Bridge command line tool adb

Install [options]
<PATH> Installs a package (specified by <PATH>) to the system.

Options:

- -l: Install the package with forward lock.
- -r: Reinstall an exisiting app, keeping its data.
- -t: Allow test APKs to be installed.
- -i <INSTALLER_PACKAGE_NAME>: Specify the installer package name.
- -s: Install package on the shared mass storage (such as sdcard).
- -f: Install package on the internal system memory.
- -d: Allow version code downgrade.

[Ref](https://developer.android.com/studio/command-line/adb)
