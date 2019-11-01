# UWC VPN

To access the Meerkat Cluster account creation portal and to connect to the Meerkat Cluster the user must be connected to the UWC VPN.

## Download the VPN client

### Windows and Mac users

To download the GlobalProtect VPN client, go to https://vpn.uwc.ac.za.

Log in to the GlobalProtect Portal using your UWC network credentials (Novell login credentials). If you are uncertain about these credentials please contact servicedesk@uwc.ac.za for information.

<img src="http://docs.meerkat.uwc.ac.za/_media/vpn1.png" alt="GlobalProtect Portal login" width=500 />

Download the relevant GlobalProtect agent depending on your operating system.

<img src="http://docs.meerkat.uwc.ac.za/_media/vpn2.png" alt="GlobalProtect by OS download" width=500 />

Install the VPN client. After the installation is complete, open the GlobalProtect VPN client. Type the VPN portal address vpn.uwc.ac.za in the input field and clidck "Connect".

<img src="http://docs.meerkat.uwc.ac.za/_media/vpn3.png" alt="GlobalProtect portal address" width=500 />

Enter your network credentials and then click "Sign In".

<img src="http://docs.meerkat.uwc.ac.za/_media/vpn4.png" alt="GlobalProtect sign in" width=500 />

The status of the GlobalProtect VPN client should change to "Connected".

<img src="http://docs.meerkat.uwc.ac.za/_media/vpn5.png" alt="GlobalProtect status" width=500 />

### Linux users

For Linux users the opensource openconnect VPN client works with the Palo Alto firewall.

On Ubuntu 18.04:

```
sudo apt-get update
sudo apt-get install openconnect
sudo openconnect --protocol=gp -u <UWC network username> --passwd-on-stdin vpn.uwc.ac.za
```

You will be prompted to enter your password.