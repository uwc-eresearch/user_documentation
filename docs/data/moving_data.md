# Copying data from inside of the SANBI network to outside (vice versa)

You might find yourself in the need to move data from a server inside of the SANBI network to your local machine, you vice versa.

Since `gate.sanbi.ac.za` does not contain any user data (for security purposes), you will need to create a tunnel through gate to access a server inside of the SANBI network directly. To do this, use the following command:

```bash
ssh -L<port_number>:queue00.sanbi.ac.za:22 <username>@gate.sanbi.ac.za
```
Replace <port_number> with a random 4 digit number and <username> with your SANBI system username.

Once this is done, you will be logged into the `gate` machine like a normal SSH session. You can now open a new terminal and type:

```bash
scp -P <port_number> <username>@127.0.0.1:<remote_directory_or_file_to_copy> <location_on_your_computer_to_place>
```
Replace <port_number> and <username> with the number and name you entered earlier, <remote_directory_or_file_to_copy> with the full directory of the data you want to copy from SANBI and <location_on_your_computer_to_place> with the directory you want to place to data on your local computer.

The reverse can be done to place a file in the SANBI network:

```bash
scp -P <port_number> <location_on_your_computer_to_place> <username>@127.0.0.1:<remote_directory_or_file_to_copy>
````

For example:

I want to copy a file `datafile.tar.gz` from my `/usr/people/eugene` directory on the SANBI cluster. I would do the following:

1. Open a terminal and type:

```bash
ssh -L1234:queue00.sanbi.ac.za:22 eugene@gate.sanbi.ac.za
```

2. Open a new terminal and type:

```bash
scp -P 1234 eugene@127.0.0.1:/usr/people/eugene/datafile.tar.gz ./datafile.tar.gz
```
The file will now be copied straight to my computer.
