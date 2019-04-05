# Logging in to the SANBI cluster head node

To use the SANBI compute cluster you need to first log in to the head node, a computer called **queue.sanbi.ac.za** or **queue**. You can only do this when you are on the SANBI network* (whether you are on the cable network at SANBI or using the SANBI VPN) and how you do this will depend on what operating system your computer is running: ___Linux___, ___MacOS___ or ___Windows___. Before this you need to know your SANBI cluster username and password.

\* _There is currently an issue with the WiFi network that will not allow you access to queue._

The two steps of connecting are opening a `terminal` and then making the connection. These steps are somewhat similar on Linux and MacOS, but a little different on Windows.

## Linux/MacOS

### Opening a terminal

The `terminal` application will act as your portal to connect to the SANBI cluster and issue it with commands.

#### On Linux

If you are running ___Ubuntu Linux___ (which is the supported operating system at SANBI) you need to open the `terminal` application. There are two ways to do this. The quickest it the key combination **Control-Alt-T**. Hold down those three keys together and `terminal` will open.

The second way is via the graphical interface. This can be opened by pressing the _Super (Windows/Start)_ key on your keyboard, which looks like this:

![CTRL/SUPER/ALT keys](../_media/ctrl_super_alt.jpg ':size=50%' )

Then type `terminal` to search for the application and click on it to start the application.

#### On MacOS

To open a `terminal` on MacOS open Spotlight search (for example by holding down _Command-Space_) and type `terminal` to search for the `terminal` application and click on it to start the application.

### SSH to queue

In your `terminal` application type the command:

```bash
ssh <username>@queue
```

The **username** should be your SANBI cluster username. These usernames are based on the first letter of your first name and your complete surname, e.g. **edebeste**. If your username does not work, please check with IT that your account is activated.

You may receive a warning message like this:

```bash
The authenticity of host 'queue00 (192.168.2.42)' can't be established.
ECDSA key fingerprint is e4:87:c2:ca:5e:57:8b:1a:83:44:a4:b5:2d:11:aa:31.
Are you sure you want to continue connecting (yes/no)?
```

Type "**yes**" to continue connection. You will get this warning message every time you connect to a computer for the first time. You will now be asked for your password. Assuming the username was **edebeste**, as per the example, it should look like this:

```bash
edebeste@queue's password: 
```

Enter your SANBI cluster password and press **Enter**. You should now see output like the following:

```bash
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.15.0-46-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

83 packages can be updated.
0 updates are security updates.

New release '18.04.2 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

edebeste@queue:~$
```

The _@queue_ after your username shows that you are now connected to the computer named _queue_ and any commands that you type will run on this computer. Always look out for this _@queue_ so that you know you are connected to the correct computer.

## Windows

### Using PuTTY

THIS SECTION IS WIP
