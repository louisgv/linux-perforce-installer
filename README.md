# About

This script will install Perforce Server on a 64-bit linux host.

# Usage

In shell, run the following commands in your terminal. You don't need to download this repo, that is what the first line in the following code does.

```shell
wget https://raw.githubusercontent.com/louisgv/linux-perforce-installer/master/install-perforce
chmod +x install-perforce
sudo ./install-perforce
```

You will be asked to create a password and user details for a new unprivileged system user named `perforce`. You generally will never need to ever log into your server with this user, but I still suggest a password you won't lose. This is *not* a Perforce user, this is a Linux/Ubuntu user for the server only. You will create your Perforce user when you connect for the first time.

Afterwards, the server will restart and you should then be able to connect to your Perforce server.

# Security

The created server will have default Perforce installation settings. This means anyone who connects to your server can create a user account without authorization. After you create your first user, you should close this security hole by using the following `p4` command from your Perforce Client.

        p4 configure set dm.user.noautocreate=2

        p4 configure set run.users.authorize=1

        p4 configure set dm.keys.hide=2

        p4 set P4IGNORE=.p4ignore

        p4 typemap

```
# Perforce File Type Mapping Specifications.
#
#  TypeMap:             a list of filetype mappings; one per line.
#                       Each line has two elements:
#
#                       Filetype: The filetype to use on 'p4 add'.
#
#                       Path:     File pattern which will use this filetype.
#
# See 'p4 help typemap' for more information.

TypeMap:
                binary+w //depot/....exe
                binary+w //depot/....dll
                binary+w //depot/....lib
                binary+w //depot/....app
                binary+w //depot/....dylib
                binary+w //depot/....stub
                binary+w //depot/....ipa
                binary //depot/....bmp
                text //depot/....ini
                text //depot/....config
                text //depot/....cpp
                text //depot/....h
                text //depot/....c
                text //depot/....cs
                text //depot/....m
                text //depot/....mm
                text //depot/....py
                binary+l //depot/....uasset
                binary+l //depot/....umap
                binary+l //depot/....upk
                binary+l //depot/....udk
```

Source: https://docs.unrealengine.com/en-us/Engine/Basics/SourceControl/Perforce
