# UWC VPN

To access the Meerkat cluster account creation portal you must either be on a wired connection on UWC campus or be connected to the UWC VPN.

If you cannot access the Meerkat cluster account creation portal at http://pubkeys.uwc.ac.za:3000 try downloading the UWC VPN client.

## Download the VPN client

### Windows and Mac users

To download the GlobalProtect VPN client, go to https://vpn.uwc.ac.za.

Log in to the GlobalProtect Portal using your UWC network credentials (Novell login credentials). If you are uncertain about these credentials please contact servicedesk@uwc.ac.za for information.

<div style="text-align:center"><img src="http://docs.meerkat.uwc.ac.za/_media/vpn1.png" alt="GlobalProtect Portal login" width=275 /></div>

Download the relevant GlobalProtect agent depending on your operating system.

<div style="text-align:center"><img src="http://docs.meerkat.uwc.ac.za/_media/vpn2.png" alt="GlobalProtect by OS download" width=450 /></div>

Install the VPN client. After the installation is complete, open the GlobalProtect VPN client. Type the VPN portal address `vpn.uwc.ac.za` in the input field and clidck "Connect".

<div style="text-align:center"><img src="http://docs.meerkat.uwc.ac.za/_media/vpn3.png" alt="GlobalProtect portal address" width=275 /></div>

Enter your network credentials and then click "Sign In".

<div style="text-align:center"><img src="http://docs.meerkat.uwc.ac.za/_media/vpn4.png" alt="GlobalProtect sign in" width=375 /></div>

The status of the GlobalProtect VPN client should change to "Connected".

<div style="text-align:center"><img src="http://docs.meerkat.uwc.ac.za/_media/vpn5.png" alt="GlobalProtect status" width=275 /></div>

### Linux users

For Linux users the opensource openconnect VPN client works with the Palo Alto firewall.

On Ubuntu 18.04:

```
sudo add-apt-repository ppa:dwmw2/openconnect
sudo apt-get update
sudo apt-get install openconnect
openconnect --protocol=gp vpn.uwc.ac.za
```

You will be prompted to enter your UWC Network username and password. The UWC Network name will be the same as the username for other UWC services, such as iKamva.
