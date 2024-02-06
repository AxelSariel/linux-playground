# linux-playground
General scripts and aliases I use in my linux environments

## System Services
To run applications as system service

### Autossh Reverse Tunnel
1. Install autossh with `sudo apt install autossh`
2. Create service file `sudo nano /etc/systemd/system/tunnel-service.service`
3. Paste the following, where 9997 is remote port and cakes is the remote host config in ~/.ssh; make sure you put your specified user
```
[Unit]
Description="SSH Reverse Tunnel Service"
After=network-online.target ssh.service

[Service]
Type=simple
User=pi
Restart=always
RestartSec=5
ExecStart=/usr/bin/autossh -M 0 -o ExitOnForwardFailure=yes -N -R 9997:localhost:22 cakes

[Install]
WantedBy=multi-user.target
```
4. Install service with `sudo systemctl enable tunnel-service.service`
5. Start service with `sudo systemctl start tunnel-service.service`
6. From your remote computer, ssh into the reversed tunnel computer by `ssh user@localhost -p 9997`
