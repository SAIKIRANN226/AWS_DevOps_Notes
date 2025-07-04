### How to connect to Private Instances using VPN ?
1. Install "OpenVPN" software in your laptop.
2. In AWS account we have two VPC's 1.Default_VPC & 2.Roboshop_VPC, make sure to have peering connection
   between these two.
4. Install VPN in "Default_VPC"
5. Obviously we have Private instances in "Roboshop_VPC"
6. Now traffic is routing as below.
7. Home-Laptop(Through OpenVPN) ---> VPN(In default_VPC) ---> Private_Instance(In Roboshop_VPC)
8. Security_group rule should be ---> OpenVPN should accept connections from Home ---> Mongodb(Private
   instances) should accept connections from VPN.
9. Make sure to enable VPN in all the Private_instances.

Since they are Private servers, they dont have PublicIP to connect. According to the diagram, connection is coming from VPN to the mongodb, so we need to enable VPN in mongodb by going to the mongodb_SG/Edit_inbound rules/Add_rule_SSH, since it is secure connection, and from where it should be opened ? it should be opened from whichever SG is attached to the VPN, that SG should be given in the source, because vpn IP is dynamic. It is changing everytime, so we are giving SG of VPN_instance (which we have created "open-vpn" instance below). Now take mongodb PrivateIP and try to connect in the super putty. If connected, we successfully connected to the Private ec2 through VPN from our home-network to the aws-network.
- Create one Public_instance (name it like "open-vpn" as your wish) for VPN in Default_VPC and allow-all for
  for security group while creating instance. 
- Connect using super putty with PublicIP.
- Search in google "openvpn install" and use "angristan" person who written script to install openvpn.
- Run the shown commands in the server by taking sudo access "sudo su -"
- It will prompt to provide the PublicIP_address/NO_for_IpV6/default_port/TCP/any_DNS/NO_for_compression/NO
  for encryption.
- Client name :- Give any name like "saikiran"
- Select passwordless client, which means its a key type.
- ls -l, you can see like "saikiran.ovpn"
- Download OpenVPN software from google for windows.
- Open "OpenVPN-connect" in your laptop.
- Cat saikiran.ovpn, copy and save it as file in notepad++ in your local with file type as all_types, this
  file is nothing but authentication file, everything is there here only, like username or password etc.
- Add or upload this file in openvpn connect by pressing + and connect.
- Then try to connect your Private instance in super putty using PrivateIP.

### Now automate the above process using terraform code
- Go through the code of 03-vpn in |VS|.

### Points to remember
- Configuring VPN is not our responsibility, we have separate team for this, in companies mostly they use
  cisco_vpn, but right now we are using open-vpn which is free and open-source.
- According to the diagram we have Default_VPC and Roboshop_VPC and we installed vpn in default_vpc, so that
  means there should be a peering connection between these two VPC's then only able to connect to Private ec2.
- If you feel slow while doing terraform commands like init, plan, apply in gitbash. It may be because of vpn.
  So disconnect vpn and try.
- And incase if your Private ec2 like mongodb is unable to connect in super putty that means you dint given
  ami_id, while creating instances and bydefault it is trying to take "aws-linux"
