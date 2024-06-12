# SNORT
Basic Network Intrusion Detection System 

Snort: Your Free and Open-Source Network Intrusion Detection System (NIDS)

---

# Snort Installation and Configuration on Ubuntu

## Installation

To install Snort, run:
```sh
$ sudo apt-get install snort -y
```

During installation, the 'Configuring Snort' window will appear. You need to specify which interface Snort will listen to.

Open a new terminal window and use:
```sh
$ ifconfig
```
![WhatsApp Image 2024-06-12 at 20 01 38_a7a0e9e6](https://github.com/ShashankRaut1604/SNORT/assets/157049159/442b287b-505d-42f5-9be2-7e86eb7fa5f2)

All available interfaces will be listed. Select your choice and specify it in the 'Configuring Snort' window (e.g., `enp0s3`).

![WhatsApp Image 2024-06-12 at 19 47 46_5aed6387](https://github.com/ShashankRaut1604/SNORT/assets/157049159/fe29937e-b369-49fd-9f22-bcbdc5cdc068)


Proceed to the next window, which will ask for the 'Address range for the local network'. Specify the network address displayed by the `ifconfig` command (e.g., `192.168.2.0/24` for the selected interface).

![WhatsApp Image 2024-06-12 at 19 59 47_2f0a1c92](https://github.com/ShashankRaut1604/SNORT/assets/157049159/c302428a-93d3-4d3b-bc46-d8e1a35cdcef)


When the 'Configuring Snort' window appears again, keep the same interface as above and press enter.

Your Snort installation is now complete. To check, use:
```sh
$ snort --version
```

## Enable Promiscuous Mode

If using a virtual machine, go to Network Settings -> Advanced Settings -> Promiscuous Mode -> Allow All.

If not using a virtual machine, type:
```sh
$ sudo ip link set interface_name promisc on
```
Press enter.

For more features, type:
```sh
$ man snort
```

## Configuration

Switch to privileged mode:
```sh
$ sudo su
```

Navigate to the Snort directory:
```sh
$ cd /etc/snort
```

List all files with their permissions:
```sh
$ ls -al /etc/snort
```

The `snort.conf` file is important for configuring Snort. As a beginner, it is suggested to make a duplicate file to avoid disturbing the original configuration:
```sh
$ cp current_file_name new_file_name
```

Open the configuration file with `vim`:
```sh
$ sudo vim /etc/snort/snort.conf
```

If `vim` is not installed:
```sh
$ sudo apt-get install vim
```

In Step 1: Set Network Variables

Under 'Setting network address you are protecting', change:
```sh
ipvar HOME_NET any
```
to:
```sh
ipvar HOME_NET 192.168.2.0/24
```

In Step 7: Customize Your Rule Set

You can keep the default set of rules available with Snort. You can also add or remove rules according to your needs.

### Validate Configuration

To validate the configuration for Snort Network Intrusion Detection System on your machine, run:
```sh
$ sudo snort -T -i enp0s3 /etc/snort/snort.conf
```

If an error occurs in the rules file, comment out the unnecessary rules and keep the `local.rule` file for reference.

### Execute Snort

Once the configuration is validated, to run Snort, use:
```sh
$ sudo snort -A console -q -u snort -g snort -c /etc/snort/snort.conf -i enp0s3
```

Now, with monitoring enabled on the Ubuntu machine, use Parrot OS to perform a network map:
```sh
$ nmap 192.168.2.1
```
You will see the generated alert log.

---
