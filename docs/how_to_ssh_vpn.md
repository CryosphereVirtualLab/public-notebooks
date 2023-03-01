The followings are needed in order to connect to a server running in a jupyter notebook:

    A PTEP dev. VM at https://www.polartep.io/ssoportal/pages/p_devTest.jsf
    The server software running in a jupyter notebook at www.polartep.io/jupyter
    A reverse port forwarding ssh tunnel between the dev. VM and the notebook
    VPN connection between the user's PC and PTEP net.


Instructions

VM preparation:

    Create a PTEP dev VM if you don't have one already.
    Identify its IP address. (will be referenced as <PTEP-VM-IP> in this doc.)
    Login via SSH
    Gain root access:
        execute: sudo su
    Configure the SSH service so that it accepts bind address configuration from remote client:
        execute: sed -i 's/#GatewayPorts.*/GatewayPorts clientspecified/' /etc/ssh/sshd_config
        execute: service sshd reload
    Open the <SERVICE-PORT> on the firewall:
        execute: ufw allow <SERVICE-PORT> (e.g.: ufw allow 3193)


Jupyter notebook preparation:

    Start the server software ina jupyter notebook, identify the port it listens on (e.g.: 3193 from the email below, referenced as <SERVICE-PORT>)
    Open a terminal in the jupyter notebook
    Connect to the PTEP VM we prepared in the previous step:
        execute: ssh -R 0.0.0.0:<SERVICE-PORT>:localhost:<SERVICE-PORT> <PTEP-USERNAME>@<PTEP-VM-IP>
        (e.g.: ssh -R 0.0.0.0:3193:localhost:3193 bakcsa@172.16.0.13)


Connecting to the service:
Open a browser on your local machine and go to http(s)://<PTEP-VM-IP>:<SERVICE-PORT>/

http/https depends on the service running in the notebook. Most probably http.
