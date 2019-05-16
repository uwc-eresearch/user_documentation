# Connecting to Eduroam with UWC credentials

`eduroam` allows staff from UWC to connect to a WiFi network at any institution offering an eduroam access point. It does this by routing your authentication request to your home institution, i.e. it knows that `@uwc.ac.za` means UWC. To use this you need:

1. Your UWC identity: Novell or original username and password. This is the same username and password that you use to access email or Novell services. __If you are unsure what this is, please contact servicedesk@uwc.ac.za__.
2. A computer with WPA2 Enterprise support. Googling suggests that this works on some versions of Windows, MacOS, Linux and Android.

## MacOS X

To use `eduroam` on a Mac you need to install the UWC eduroam profile.

Go to https://cat.eduroam.org/. From here, select the "_Click here to download your eduroam® installer_" button. Wait for the pop-up box to load and select "University of the Western Cape". When the page is loaded, click the download button for your installer. Once the page loads you should see a download occur, this download should end in `.mobileconfig`.

Download the [profile file](http://docs.wp.sanbi.ac.za/?attachment_id=45) and save it as **sanbi\_eduroam.mobile.config**. Double click to install it and a System Settings window will open, asking you to enter your username and password (**Your gateway login password, NOT email password!**) for the profile (just use your plain username – i.e. **_myuser_**, not **_myuser@sanbi.ac.za_**). You **don’t** need to enter these at installation time. If you _do_ enter them now, but you make a mistake, you will have to delete this profile and start again. If you _don’t_ enter your username and password at this stage, you will be asked for them when you connect to eduroam.

After you add the profile, you will be asked to authorise the change that you’re making to your system settings. Once that’s done, you’ll be able to connect to eduroam from your Mac.
