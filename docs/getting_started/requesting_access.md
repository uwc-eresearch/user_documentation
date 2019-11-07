# Requesting access

To request an account on the Meerkat cluster, go to http://pubkeys.uwc.ac.za:3000.

Log in with your UWC network credentials. 

This is a Gitea service where you will have a user profile for the Meerkat cluster. Here you can manage your ssh keys and request access to the Meerkat cluster.

## Upload your ssh public key

An ssh key pair is used for authentication when logging into the Meerkat cluster. When you create a ssh key pair you create a private and public key. Never share your private key with anyone. Follow these [instructions](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) to generate an ssh key pair.

On the Gitea portal:

* Click `Profile and Settings` (your portait) -> `Settings`. 
* Go to the `SSH / GPG Keys` tab. 
* Under the `Manage SSH Keys` section, click `Add Key`. 
* Copy the contents of your ssh public key file to the `Content` input field. On a Linux or Mac system your public key will generally be stored at `~/.ssh/id_rsa.pub`
* Click `Add Key` (green button) to save your key.

## Apply for access to the Cluster

On the Gitea portal:

* Click `Explore` at the top left of the page.
* Go to `hpc1 / repo1` -> `Issues` -> `New Issue`.
* In the `Title` field enter "join" and click `Create Issue`.

The cluster administrators will be alerted and will confirm your access to the Meerkat cluster.