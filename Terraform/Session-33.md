### How to connect to private instances using VPN ?
![Screenshot 2025-06-04 225101](https://github.com/user-attachments/assets/6df4a952-3eec-4e72-9c53-bd6e21df09c7)
From the above diagram, Now connection is comming from VPN to the mongodb, so we need to enable VPN in mongodb
by going to the mongodb_SG/Edit inbound rules/Add rule of SSH, and from where it should be opened ? it should 
be opened from which ever SG is attached to the VPN, that SG should be given in source, because vpn IP is dynamic, so we are giving SG of VPN_instance (which we have created open-vpn instance below). Now take mongodb
private_ip and try to connect in the super putty, if connected we successfully connected to the private ec2
using VPN from our home-network to the aws-network.

- Create one public_instance (name it like "open-vpn" as your wish) for VPN in default_VPC and allow-all for
  for security group while creating instance. 
- Connect using super putty with public_ip
- Search in google "openvpn install" and use angristan one who written script to install openvpn.
- Run the shown commands in the server with sudo access.
- It will prompt to provide the public_ip address/NO for IpV6/default port/TCP/any DNS/NO for compression/NO
  for encryption.
- Client name : give any name like "saikiran"
- Select passwordless clinet, which means its a key type.
- ls -l, you can see like "saikiran.ovpn"
- Install open-vpn client from google for windows, name will be "openvpn connect"
- Open open-vpn connect in your laptop.
- cat saikiran.ovpn, copy and save it in notepad++ and save as a file in your local with file type as
  all_types, this file is nothing authentication file, everything is there here only like username or password
- Add or upload this file in openvpn connect by pressing + and connect.

### Now automate above all those using terraform code
- Go through the code of 03-vpn in |VS|





















### Points to remember
- Configuring vpn is not our responsibility, we have separate team for this, in companies mostly use cisco vpn
  but right now we are using open-vpn which is free and open-source
