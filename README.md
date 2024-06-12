# Azure Virtual Networks

## Objective

In this lab, To navigate to an Azure VPN gateway, which is a kind of Virtual Network Gateway. to learn what it does, and why i might choose to use one. To learn how a VPN gateway handles traffic to and from a separate network. Lastly, simulate the creation of a Site-to-site connection to an artificial local network gateway.

### Skills Learned

- Run SQL queries to retrieve information from a database
- Advanced understanding of how to apply AND, OR, and NOT operators to filter SQL queries

### Tools Used

- Azure
- Azure Gateways
- Azure VPN
- Azure virtual Networks

## Step 1 - Reviewing Azure Virtual Networks

I have opened up the 'All Resources' menu and selected the calabs-vnet resource page

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/c3e5dfb1-d535-4945-b4d2-1fa1022b6f31)

There are a few things to be aware of in this section:

- Like other resources in Azure, the virtual network has a Resource group ID and a Subscription ID. This means that the virtual network belongs to a specific resource group and Azure subscription. To quickly summarize, resource groups and subscriptions are two tools Microsoft uses to organize, track and bill for its resources.
- The network also has a Location, which is the geographical region that holds the servers your network is hosted on.
- Finally, the network has an Address space of 10.0.0.0/16, meaning any resource that is deployed under this virtual network and which is capable of having an IP address will have an address inside this address space. Also, note that because 10.0.0.0/16 is a private address range, this network currently only hosts private resources.

selecting the connected devices menu option we can see there are currently two Network Interfaces connected to this VNet. Notice a couple of things about each connected resource:

- Each resource has an IP Address that falls within the address range we saw earlier.
- Each resource also belongs to a subnet.

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/7eb07486-0761-448d-8358-739da484dfdf)

Next we click on the 'Subnets' menu option.

A subnet is a way to further separate a VNet into smaller segmented networks. Subnets are used to increase the amount of organization and trackability of resources. Because you can apply different network security groups to different subnets, using subnets also potentially increases the security of your infrastructure.

Notice that there are two subnets on the Subnets blade and that each one has an Address range that falls within the address range of the VNet.

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/d4b451d7-8f28-4aed-ab98-38326c91c292)

If we go back to the Connected devices blade and click nic0 and the select caLabsVM0

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/e87a9885-11e3-4973-b4a1-419cef455510)

We are brought to the Overview blade of the caLabsVM0 Virtual Machine (VM). This is because the network interface deployed to the VNet was attached to this VM. Network interfaces allow resources including VMs to communicate with other resources in Azure and on the Internet. Because this VM has a network interface attached and that network interface belongs to the VNet, this VM will be able to communicate with other resources in the VNet.

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/227a125b-cd12-4a04-941f-523d4131615c)



## Step 2 - Reviewing Azure VPN Gateways

Azure VPN Gateways are a type of Azure Virtual network Gateway which allows you to create secure connections between your on-premises network and an Azure Virtual Network (VNet). Azure uses leading security practices to protect data traveling between your on-premises network and your Azure network as if it were a single virtual private network (VPN). Among the benefits of this is the ability to use a hybrid infrastructure consisting of cloud and on-premises resources, with more security than you would get by simply handling your traffic over the public internet.

Lets search for Local Network Gateway from the main search bar

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/5f7d5085-80cb-452a-a7b0-b392e35f54de)

The after clicking create we will add in all the required details as pictured below

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/49a51180-9543-471a-b314-08bb492a5647)

- The IP address field would contain the public IP address of the gateway of your on-premises network. Just like your VPN Gateway needed a public IP address so that your on-premises resources know how to find it, the opposite is true. The public IP address here will tell your VPN gateway where to send traffic when transmitting data to your local network.
- The Name field is where you would place a unique label on your connection, for easy organization.
- The Address space is the range of IP addresses used in your local network. This address space must not overlap with the range used by the Azure virtual network

Clicking on 'Create' we wait a little until we get the green 'Your deployment is complete' message.

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/9d614321-447e-4e70-bc5a-12991e047907)

Under the main menu and 'All Resources' we select 'calabsGateway' and can see a few things on the resulting Overview blade

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/d037a0c3-a781-4d27-8920-13c23d435362)

- The gateway has a Gateway type of VPN, know that virtual network gateways can have more than one type.
- The VPN gateway has been provisioned within a Virtual network, specifically the one we reviewed earlier. This means that by default, any traffic sent through the gateway will end up in this specific VNet until directed elsewhere.
- The gateway also has a Public IP address. VPN gateways need a public IP address because although they create an environment that emulates a private network between your on-premises resources and your cloud resources, the traffic still technically needs to travel over the public internet to reach your VPN gateway. Once configured, your on-premises network will know to send its traffic to this public IP address.

Lets set up a connection.

Clicking on 'Connections' then 'Add' we create a new site to sire connection

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/9b2005bb-2f1a-41c3-86eb-69353158b4a9)

![image](https://github.com/MattAllan1/Azure-Virtual-Networks/assets/172419505/bf353480-3d3e-46c8-9e4e-c2c174747eb2)

For site-to-site connections, notice two main data points here:

- The blade has a Virtual network gateway section set to calabsGateway, the gateway we're currently navigated to, and you can't change it. This means that you're attempting to create a connection from somewhere to your current VPN gateway.
- The blade also has a Local network gateway section, which is the section that would contain information about the local network (such as your on-premises network) that you wish to connect to your VPN gateway.







