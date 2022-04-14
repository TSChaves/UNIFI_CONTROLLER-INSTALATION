# UNIFI CONTROLLER

This article provides the steps to update the UniFi Network application to the current stable release on a Debian or Ubuntu system via APT (Advanced Package Tool).

## Requirements
In order to update the UniFi Network application via APT, it is necessary to create source files or edit lines in an existing sources.list file with Linux text editors: vi or nano. The repo structure should be permanent, but if there are any changes they will be pointed out in the UniFi Network software version release posts, found in the Release section of the Community.

Before upgrading the UniFi Network application, make sure that you have backed up the UniFi Network Database. You will need to make sure that the user has sudo permissions. For more information about adding a user to sudo list, see this Debian article.

## UniFi Network APT Steps

**1.** Install required packages before you begin with the following command:

```bash
sudo apt-get update && sudo apt-get install ca-certificates apt-transport-https
```

**2.** Use the following command to add a new source list:

```bash
echo 'deb https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt-unifi.list
```

**3.** Add the GPG Keys. To add the GPG Keys use one of the two methods described below (**Method A is recommended**). When using the commands below, it is assumed you have **sudo** and **wget** installed.

**User Tip:** For Ubuntu 18.04, run the following commands before installing UniFi in step 4.

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-3.4.asc | sudo apt-key add -
echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
sudo apt-get update
```

**(Method A)** Install the following trusted key into */etc/apt/trusted.gpg.d*

```bash
sudo wget -O /etc/apt/trusted.gpg.d/unifi-repo.gpg https://dl.ui.com/unifi/unifi-repo.gpg 
```


**(Method B)** Using apt-key.

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50 
```

**4.** Install and upgrade the UniFi Network application.

**Note:** *On some Distributions, it's possible an incompatible Java release can be installed during this step. We recommend running the following command before proceeding with this step, to restrict Ubuntu from automatically installing Java 11. If you wish to undo this later, replace "hold" with "unhold".*

```bash
sudo apt-mark hold openjdk-11-*
```

Install and upgrade the UniFi Network application with the following command:
```bash
sudo apt-get update && sudo apt-get install unifi -y
```
**5.** The UniFi Network application should now be accessible at the computer's configured local or public IP address, by typing that IP address in a browser's navigation bar (Chrome is recommended). If it is not launching, use the following command: **sudo service unifi start**.

**Other helpful commands are:**
* To stop the UniFi service:
```bash
 sudo service unifi stop
```

* To restart the UniFi service:

```bash
 sudo service unifi restart
```

* To see the status of UniFi service: 

```bash
sudo service unifi status
```

# Log Files Location

* /usr/lib/unifi/logs/server.log
* /usr/lib/unifi/logs/mongod.log

If your application is running on a Unix/Linux based system, then you will require superuser (**sudo**) privileges to access these log files.
