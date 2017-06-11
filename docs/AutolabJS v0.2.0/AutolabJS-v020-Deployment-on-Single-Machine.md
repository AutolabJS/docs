# v0.2.0 Deployment on Single Machine

## Prerequisite

1. Ubuntu server 16.04 operating system.
2. Record the IP Address / domain name of the machine. If your machine has multiple IP addresses, please use the public IP address for installation purposes. Because of ease of use, domain name (DNS) is a preferred option for hostname in all the configuration files.
Most likely, your machine may be on a corporate private network with a gateway / proxy server / firewall connection to Internet. In that case, please use your machine's private ip address.
You can locate the configured IP address of your machine using the following command.
    ```
    ip addr show
    ```
    in the displayed output, look for IP address following the **inet** keyword.

3. Change the listening port of SSH server to 2222 in `/etc/ssh/sshd_config` file and restart the SSH server using the following command.  
`sudo service ssh restart`  
If the SSH server is not running on your machine, please ignore the rest of this section and directly go to [**Installation**](#installation) section.
4. For the SSH setting to be fully effective, logout of the current SSH session and relogin.

## Installation

1. Clone Repository  
`git clone https://github.com/AutolabJS/AutolabJS.git`

2. Change to deploy directory  
`cd AutolabJS/deploy`

3. Execute setup script  
`./setup.sh`

4. Configure the AutolabJS components by editing the configuration files in `deploy/configs/<component>`. Note that you need to use `localhost` for IP address of the machines wherever required. Unless you have special requirements, you can use the default host(name) and port numbers.  
The list of configuration files to be changed are:  
**deploy/configs/main_server:** APIKeys.json, conf.json, courses.json, labs.json  
**deploy/configs/load_balancer:** nodes_data_conf.json  
**deploy/configs/execution_nodes:** scores.json, conf.json  

5. Do remember to change the default passwords in both the inventory file (`AutolabJS/deploy/inventory`) and in the configuration files. Please make sure that the changed passwords match in both the inventory file and the configuration files.
The locations of credentials are:  

	|File											   |MySQL |GitLab |Main Server|
	|--------------------------------------------------|------|-------|-----------|
	|deploy/inventory								   |	✔ |	✔	  |           |
	|deploy/configs/main_server/APIKeys.json 		   |	  |	      |✔ (for /admin route)|
	|deploy/configs/main_server/conf.json			   |	✔ |	  ✔   |           |
	|deploy/configs/load_balancer/nodes_data_conf.json |	✔ |       |           |

6. In the `gitlab` section of inventory file, change the hostname of **gitlab** item from **localhost** to **Machine IP / domain name**. If the machine has multiple IP addresses, then please use the public IP address. The line should look like  
	```
	
	[gitlab]    

	<Machine_IP> ansible_connection=local ansible_python_interpreter=/usr/bin/python2 gitlab_password=<gitlab_password>

	```

7. Run the ansible-playbook:  
`sudo ansible-playbook -i inventory playbook-single.yml`  
The username and the password to be provided are the credentials of root user (or sudoer) of the machine.

8. Ansible installs all the components of AutolabJS. If the previous step executes successfully, the **installation is complete**.

9. Add cron job to restart the AutolabJS components automatically.

    1. Login as root  
    	`sudo su`
    2. Copy restart script to root account  
   		`cp deploy/autolab-restart.sh /root/`
    3. Open crontab editor as root user  
		`crontab -e`
    4. Enter a job in the file to run the restart script every minute.  
		`* * * * * bash /root/autolab-restart.sh`

10. In case of installation failure due to incorrect configuration, please see the FAQ page to see if you can resolve the error. If not, you can run the following commands to uninstall AutolabJS.

    1. The uninstall command is:  
		`sudo ansible-playbook -i inventory uninstall.yml`  
		The username and the password to be provided are the credentials of root user (or sudoer) of the machine.

    2. Remove the previously generated SSH keys  
		`rm -f AutolabJS/deploy/keys/main_server/*`  
		`rm -f AutolabJS/deploy/keys/load_balancer/id_rsa*`  

    3. Repeat the installation step-(7) given above to install AutolabJS again.

11. Installation creates containers for main server, load balancer, execution node, data base and Gitlab. For further information on managing these containers see [container maintenance](#) page.
