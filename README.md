# linux-playground
General scripts and aliases I use in my linux environments

## System Services
To run applications as system service

### Autossh Reverse Tunnel
Where 9997 is remote port and cakes is the remote host config in ~/.ssh

```
[Unit]
Description="SSH Reverse Tunnel Service"
After=network-online.target ssh.service

[Service]
Type=simple
User=pi
Restart=always
RestartSec=5
ExecStart=/usr/bin/autossh -M 12000 -o ExitOnForwardFailure=yes -N -R 9997:localhost:22 cakes

[Install]
WantedBy=multi-user.target
```
