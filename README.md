This repository is going to hold multiple examples of iptables for use as a template to get started.
Usage:
I recommend using 
$ iptables-save > outputfile.rules
and
$ iptables-restore < inputfile.rules

in order to save and restore firewall rules.  Note: depending on the system you may be able to run these as sudo, if running iptables-save as sudo yields a blank file please try running it as root (sudo su).

The more advanced rules will likely require port forwarding to be enabled, you can do so with the following (wil be undone upon reboot):
$> sudo echo 1 > /proc/sys/net/ipv4/ip_forward 

If you must specify a singular (or multiple) rules from the command line simply be sure to structure the command correctly (again, may run as sudo but if not you will need to be root).  
First identify which table that the rule is to be added to (will be between the lines containing *tablename and COMMIT where tablename could be any of the following five tables (in descending order of likelyhood) filter, nat, mangle, raw, security 
Then append the line containing the rule you want to add from the .rules files contained in this repository

An example of one of the rules from getting-started.rules that will allow all SSH traffic inbound to be accepted (be sure to run this BEFORE dropping all inbound traffic otherwise you will stop allowing your own inbound SSH connection!)
 
$ sudo iptables -t filter -A INPUT -j ACCEPT -p tcp --dport 22

Much more information can be found on the arch linux wiki page here: https://wiki.archlinux.org/index.php/Iptables#Tables
