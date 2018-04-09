# Connecting to and using the SANBI printer

SANBI uses a Samsung X4300 series printer. In order to connect to it, you require some drivers for all operating systems.

## Ubuntu

You'll need to install the Samsung Unified Linux Driver (suldr) for Ubuntu.

```bash
sudo bash -c 'echo "deb http://www.bchemnet.com/suldr/ debian extra" >> /etc/apt/sources.list'
cd ~/Downloads  
wget http://www.bchemnet.com/suldr/pool/debian/extra/su/suldr-keyring_2_all.deb
sudo dpkg -i suldr-keyring_2_all.deb
sudo apt-get update
sudo apt-get install suld-driver-4.00.39
```

When done, you'll be able to add the printer via the normal way:

1. Open the Unity dash (Windows/Start key).
2. Type `printers` and open the printer configuration tool.
3. Click the `Add` button.
4. Select `Network Printer -> Find Network Printer` and type `printer.sanbi.ac.za` under `Host:`
5. Select `AppSocket/HP JetDirect` under the `Connections` and click `Forward`, `Forward` and `Apply`.

All done!

## Windows

TBD

## MAC OS X

TBD