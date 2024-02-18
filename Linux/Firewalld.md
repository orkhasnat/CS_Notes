# Open Incoming  Ports in Firewall
In order to add rules to `firewalld`  use the `firewalld-cmd` command to add or remove rules. 
E.g. to open a specific port for **tcp(*dhcpv6-client*)** use the following command, 
```bash
	sudo firewall-cmd --add-port=<Port_Number>/tcp --permanent
	sudo firewall-cmd --reload
```
Notice that, I have added `--permanent` option to add the rule permanently.

In order to remove them use the following command,
```bash
	sudo firewall-cmd --remove-port=<Port_Number>/tcp
	sudo firewall-cmd --reload
```

> Notice that each time something is changed the `--reload` command is necessary. Otherwise it won't work at all. Only reloading, restarting the service or rebooting the PC will work as it works on either `systemd` level or kernel level. 
> >There is a command to reload the kernel module as well,
> > `--complete-reload`  even reloads the **netfilter kernel module**.
 

> [!note] Saved Rules
> The custom rules are saved in `/etc/firewalld/zones/public.xml` file.

