# Copying data to and from the Meerkat cluster

You might find yourself in the need to move data to or from the Meerkat cluster.

## Copying data from your local storage to Meerkat cluster (and vice versa)

You can copy data between your local storage on your laptop or desktop to the Meerkat cluster using `scp`. `scp` uses the same authentication and security as `ssh`, and requires a source and destination to be specified, for example, from the terminal on your laptop the following command

```bash
$ scp /path/to/source <username>@meerkat.uwc.ac.za:/path/to/destination
```
will copy the specified source file on your local storage to the specified destination on the Meerkat cluster. Note, you must have write permissions at the specified destination on Meerkat.

Similarly you can copy data from the Meerkat cluster to your local storage using

```bash
$ scp <username>@meerkat.uwc.ac.za:/path/to/source /path/to/destination
```

## Copying data from the ilifu cluster to the Meerkat cluster (and vice versa)

In order to `scp` between the ilifu cluster and the Meerkat cluster `ssh` authentication and security needs to exist between the two clusters. To set this up a user must create a new ssh key pair on the Meerkat cluster. Once you have logged in to the Meerkat cluster, generate an ssh key pair for the purposes of transferring data using the following command, replacing your email as necessary:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

You must then copy the contents of the ssh public key file to the `authorized_keys` file in your home directory on the ilifu cluster. To do this, copy the contents of the `~/.ssh/id_rsa.pub` file on the Meerkat cluster and place the contents in the `~/.ssh/authorized_keys` file on the ilifu cluster. Now you can test that `ssh` authentication between the Meerkat cluster and ilifu cluster is set up by sshing from the Meerkat cluster to the ilifu cluster, for example, from the Meerkat cluster head node:

```bash
$ ssh <username>@transfer.ilifu.ac.za
```

If this is successful we know that `ssh` and `scp` will work from the Meerkat cluster to the ilifu cluster. Exit your `ssh` session on the transfer node. You can now `scp` data from the ilifu cluster to the Meerkat cluster using `scp`. From the Meerkat cluster, you can transfer data from the ilifu cluster to the Meerkat cluster using:

```bash
$ scp <username>@transfer.ilifu.ac.za:/path/to/source /path/to/destination 
``` 

Or to transfer data from the Meerkat cluster to the ilifu cluster, on the Meerkat cluster use:

```bash
$ scp /path/to/source  <username>@transfer.ilifu.ac.za:/path/to/destination
```

Please use the `transfer.ilifu.ac.za` server when copying files to and from the ilifu cluster. **Do not use the ilifu SLURM head node to transfer data.**
