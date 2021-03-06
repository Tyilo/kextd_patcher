kextd_patcher
=============

kextd_patcher is a python script for patching the `kextd` binary to support loading of unsigned kernel extensions on OS X.

In the latest version this utility only patches `SecStaticCodeCheckValidity` to always return 0.

See [Breaking OS X signed kernel extensions with a NOP](https://reverse.put.as/2013/11/23/breaking-os-x-signed-kernel-extensions-with-a-nop/) for more info.

Dependencies
------------

The scripts uses [radare2](https://github.com/radare/radare2) to do the heavy lifting of analyzing the binary and finding which instructions should be patched. You will need to build radare2 from git and have the `r2` binary in your `PATH`.

To removing the code signature from kextd after the patching, the script uses [ldid](http://gitweb.saurik.com/ldid.git), so you will also need to have `ldid` in your path.

Usage
-----

Start by running the script:

```
$ ./kextd_patcher.py

Patched SecStaticCodeCheckValidity
Removing code signature...
Patched file is located at: /var/folders/db/kt60mzx93p110r61jzjbf3nw0000gn/T/tmpM12eNq
```

If you want to apply the patch do the following:

```
$ sudo cp /usr/libexec/kextd /usr/libexec/kextd_backup
$ sudo mv /var/folders/db/kt60mzx93p110r61jzjbf3nw0000gn/T/tmpM12eNq /usr/libexec/kextd
```

The temporary path that the script will output the patched binary to will differ, so you'll need to adjust the path in the command above.

