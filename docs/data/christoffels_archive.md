# Storing data on the Christoffels Lab archive server

For members of Professor Christoffels’ research group, you can use **smbclient** to copy files to and from the Christoffels lab archive server.

First, log into **queue00** and change directory to the directory from which or to which you want to transfer files. Connect to the archive server using:

```bash
smbclient -I 172.20.1.194 -U username '//CHRISTOFFELS IP/Documents'
```

Where _username_ is your username on the archive server (typically the same as your SANBI username). You will be prompted for your password, again note that this might be different to your SANBI password. Once you are logged in you can use the `ls`, `cd`, `lcd`, `!cd`, `mkdir`, `!mkdir`, `get` and `put` commands to move around the filesystem and retrieve and send files. E.g.

```bash
pvh@queue00:~$ smbclient -I 172.20.1.194 -U mario  '//CHRISTOFFELS IP/Documents'
Enter mario's password: 
Domain=[CHRISTOFFELS] OS=[Windows Storage Server 2008 R2 Essentials 7601 Service Pack 1]       Server=[Windows Storage Server 2008 R2 Essentials 6.1]
smb: \> ls
  .                                  DA        0  Thu Oct 23 11:33:07 2014
  ..                                 DA        0  Thu Oct 23 11:33:07 2014
  .DS_Store                          AH     6148  Thu Jun 26 11:06:26 2014
  .vss_command                       AH        0  Sat Oct 18 03:07:11 2014
  backup                              D        0  Thu Oct 23 11:32:51 2014
  xinitrc.old                         A      674  Thu Oct 23 11:19:20 2014

    44471 blocks of size 268435456. 44419 blocks available
smb: \> !ls
wcd_wrapper.sh  xinitrc.old
smb: \> get xinitrc.old
getting file \xinitrc.old of size 674 as xinitrc.old (109,7 KiloBytes/sec) (average 29,3    KiloBytes/sec)
smb: \> put wcd_wrapper.sh
putting file wcd_wrapper.sh as \wcd_wrapper.sh (31,2 kb/s) (average 31,2 kb/s)
smb: \> 
smb: \> !mkdir foo
smb: \> lcd foo
smb: \> !ls
smb: \> get wcd_wrapper.sh
getting file \wcd_wrapper.sh of size 128 as wcd_wrapper.sh (5,0 KiloBytes/sec) (average 20,6 KiloBytes/sec)
smb: \> !ls
wcd_wrapper.sh
smb: \> 
```

While **help** will show you all commands available, the most common ones are:


| Command       | Description                                               |
| ------------- | --------------------------------------------------------- |
| cd            | change directory on the archive server                    |
| lcd           | change directory on the local server (i.e. queue00)       |
| ls            | list directory on the archive server                      |
| !ls           | list directory on the local server                        |
| put           | copy a file from the local server to the archive server   |
| get           | copy a file from the archive server to the local server   |
| rm            | delete a file on the archive server                       |
| mkdir         | make a directory on the archive server                    |
| !mkdir        | make a directory on the local server                      |

## Recursive _get_ and _put_

If you want to move entire directories you can use recursive get or put operations. To do this you need to change some flags before you do your commands and because of the power of these flags we recommend not mixing them with other commands in a ‘normal’ session. We recommend: log in, do your recursive operation, log out. E.g.

```bash
pvh@queue00:~/alan$ smbclient -I 172.20.1.194 -U mario  '//CHRISTOFFELS IP/Documents'
Enter mario's password: 
Domain=[CHRISTOFFELS] OS=[Windows Storage Server 2008 R2 Essentials 7601 Service Pack 1]     Server=[Windows Storage Server 2008 R2 Essentials 6.1]
smb: \> recurse
smb: \> prompt
smb: \> mput mydir
putting file mydir/wcd_wrapper.sh as \mydir\wcd_wrapper.sh (31,2 kb/s) (average 31,2 kb/s)
putting file mydir/R/splots.rdx as \mydir\R\splots.rdx (59,6 kb/s) (average 45,4 kb/s)
putting file mydir/R/splots.rdb as \mydir\R\splots.rdb (1157,7 kb/s) (average 416,2 kb/s)
putting file mydir/R/splots as \mydir\R\splots (41,6 kb/s) (average 255,6 kb/s)
smb: \> exit
```

or

```bash
pvh@queue00:~/alan$ smbclient -I 172.20.1.194 -U mario  '//CHRISTOFFELS IP/Documents'
Enter mario's password: 
Domain=[CHRISTOFFELS] OS=[Windows Storage Server 2008 R2 Essentials 7601 Service Pack 1] Server=[Windows Storage Server 2008 R2 Essentials 6.1]
smb: \> recurse
smb: \> prompt
smb: \> mget mydir
getting file \mydir\R\splots of size 383 as splots (16,3 KiloBytes/sec) (average 16,3 KiloBytes/sec)
getting file \mydir\R\splots.rdb of size 4742 as splots.rdb (578,9 KiloBytes/sec) (average 161,4 KiloBytes/sec)
getting file \mydir\R\splots.rdx of size 244 as splots.rdx (29,8 KiloBytes/sec) (average 134,4 KiloBytes/sec)
getting file \mydir\wcd_wrapper.sh of size 128 as wcd_wrapper.sh (15,6 KiloBytes/sec) (average 114,2 KiloBytes/sec)
smb: \> exit
```

In these examples **recurse** switches recursive mode on and **prompt** switches prompting off (otherwise you will be asked whether you want to do each individual transfer). The `mget` and `mput` commands mean multiple get and put respectively.

## Network tuning for large file transfers

First, before you archive files, please compress them with `gzip`, `bzip2` or `tar` (with one of the aforementioned compression types). File types such as fastq and sam compress into a fraction of their uncompressed size. Then when you use the smbclient command add these options:

```bash
smbclient --socket-options='TCP_NODELAY IPTOS_LOWDELAY SO_KEEPALIVE SO_RCVBUF=131072 SO_SNDBUF=131072'
```

before you add the rest of the command (i.e. `-I 172.20.1.194` etc).

## Using screen to remain logged in when you are away

If you are moving a lot of data it might take some time. So start a `screen` session before you run _smbclient_. Just type `screen` and then carry on working as usual. To disconnect from the session type `Ctrl-A`, followed by the `D` key and to reconnect, log into _queue00_ and type `screen -r`. Please clean up your `screen` sessions (by logging out) when you are finished with them. [Read more about screen](http://www.tecmint.com/screen-command-examples-to-manage-linux-terminals/).