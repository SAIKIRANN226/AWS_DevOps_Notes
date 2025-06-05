### How to connect to private instances using VPN ?
![Screenshot 2025-06-04 225101](https://github.com/user-attachments/assets/6df4a952-3eec-4e72-9c53-bd6e21df09c7)
According to the diagram connection is comming from VPN to the mongodb, so we need to enable VPN in mongodb by going to the mongodb_SG/Edit inbound rules/Add rule of SSH since it is a secure connection, and from where it should be opened ? it should be opened from which ever SG is attached to the VPN, that SG should be given in the source, because vpn IP is dynamic every time is changing, so we are giving SG of VPN_instance (which we have created "open-vpn" instance below). Now take mongodb private_ip and try to connect in the super putty, if connected we successfully connected to the private ec2 through VPN from our home-network to the aws-network.

- Create one public_instance (name it like "open-vpn" as your wish) for VPN in default_VPC and allow-all for
  for security group while creating instance. 
- Connect using super putty with public_ip.
- Search in google "openvpn install" and use "angristan" person who written script to install openvpn.
- Run the shown commands in the server by taking sudo access "sudo su -"
- It will prompt to provide the public_ip address/NO for IpV6/default port/TCP/any DNS/NO for compression/NO
  for encryption.
- Client name :- give any name like "saikiran"
- Select passwordless client, which means its a key type.
- ls -l, you can see like "saikiran.ovpn"
- Install open-vpn client from google for windows, software is "openvpn connect"
- Open "openvpn-connect" in your laptop.
- Cat saikiran.ovpn, copy and save it as file in notepad++ in your local with file type as all_types, this
  file is nothing authentication file, everything is there here only like username or password etc.
- Add or upload this file in openvpn connect by pressing + and connect.
- Then try to connect your private instance in super putty using private_ip.

### Now automate above all those process using terraform code
- Go through the code of 03-vpn in |VS|.




### Points to remember
- Configuring vpn is not our responsibility, we have separate team for this, in companies mostly use cisco vpn
  but right now we are using open-vpn which is free and open-source.
- According to the diagram we have default_VPC and roboshop_VPC, and we installed vpn in default_vpc, so that
  means there should be a peering connection between these two VPC's then only able to connect to private ec2.
- If you feel slow while doing terraform commands like init,plan,apply in gitbash. It may be because of vpn.
  So disconnect vpn and try.
- And incase if your private ec2 like mongodb is unable to connect in super putty that means you dint given
  ami_id, while creating instance and bydefault it is trying to take "aws-linux"
