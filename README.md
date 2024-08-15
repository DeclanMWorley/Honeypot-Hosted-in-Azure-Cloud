---
updated: 2024-08-15 07:34:51Z
created: 2024-08-11 02:46:04Z
latitude: 21.33539090
longitude: -158.05689650
altitude: 0.0000
---

## Objective
The goal of this project was to set up and utilize a honeypot to capture and analyze malicious activities targeting a virtual machine hosted on Microsoft Azure. The honeypot used for this project was T-Pot, a multi-honeypot platform that includes several tools for threat analysis.

- **Systems Utilized:** T-Pot, Microsoft Azure Ubuntu Instance
<br>


## Setting up the Honeypot

To start things off, I created a new Debian virtual machine (VM) through the Microsoft Azure portal. To ensure that the VM was adequately resourced, I gave it a minimum of 8 GB of memory and attached a 128 GB drive. I left the default network interface configurations, as we didn't need to make any changes for our use.

With the VM created, the next step is to configure the inbound security rules. Since this is a honeypot, I created a rule allowing incoming traffic on all ports from 0 to 65535. This ensures that our honeypot will be able to capture all potential attack vectors and network activity, which can be used for detailed analysis.

Next, I accesed the VM via SSH using the PuTTY application. To do so, we needed to use the public facing IP of our VM, as well as the the authentication details that we configured during setup.



<div style="display: flex; justify-content: center; gap: 10px; max-width: 70%;">
    <img src="../_resources/c5542ebf7e7f8db84a8546e0f6bbf578.png" style="width: 100%; height: 100%; max-width: 50%; " />
    <img src="../_resources/741c02feef791605ef584a8b94861803.png" style="width: 100%; height: 100%; max-width: 50%; " />
</div>
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/ff24bd6c960c37c521f939ffe41cafc1.png" style="width: 100%; height: 100%; max-width: 35%; " />
    <img src="../_resources/bd64f174ee07698281d85193496303cc.png" style="width: 100%; height: 100%; max-width: 65%; " />
</div>

<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/6b5aab208a10404b629b62bcb14156e1.png" style="width: 100%; height: 100%; max-width: 35%; " />
</div>
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/38ac3deddb18c9390ec245526aed4d18.png" style="width: 100%; height: 100%; max-width: 35%; " />
    <img src="../_resources/74c16e42e1059dbec19d579a51d8ff9b.png" style="width: 100%; height: 100%; max-width: 65%; " />
</div>



Once logged into the Debian VM, the first action is to update the system to ensure we have the latest patches and packages. To do this, I'll run: `sudo apt upgrade -y.`

Next, we also need to install git, as it's required for cloning the T-Pot repository that we will be using. We can install git by running: `sudo apt install git.`

With git being installed, we can continue to clone the T-Pot repository from GitHub. The repository contains all of the files that we will need to set up our honeypot. Clone the repository by running: `git clone https://github.com/telekom-security/tpotce`
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/14c4e6aedc6dccf6e966f3a6764fa3a5.png" style="width: 100%; height: 100%; max-width: 50%; " />
</div>

### T-Pot Repository Cloned
After the T-Pot repository has been cloned, I navigate into the ~/tpotce/ directory to start our honeypot installation process. After attempting to run the installer with sudo, it notifies us that we need to run it as a regular user: `./install.sh --type=user`

This launches the T-Pot installation wizard. It guides us through the installation of the required dependancies and choosing what T-Pot version we would like to deploy. For this lab, I selected the T-Pot Standard / HIVE type.

During the installation process, we will also be prompted to create a web username and password. Write this down, this is important as it will be used to login to the T-Pot web interface once our installation finishes.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/69d789fea888d66814272af7671d75c3.png" style="width: 100%; height: 100%; max-width:50%; " />
    <img src="../_resources/94ee46abb73a9e68d53e664369de4487.png" style="width: 100%; height: 100%; max-width: 50%; " />
</div>
<br>
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/6d5aca2a3d33a31028936d0f95ef70f0.png" style="width: 100%; height: 100%; max-width:50%; " />
</div>
<br>
Upon completion of the installation wizard, it will prompt us to reboot our system, and that we can re-connect via SSH on tcp/64295.


<br>

## T-Pot Web Interface

Now that T-Pot is successfully setup, we can begin to explore the web dashboard, which is accessible via the public facing IP address of our VM at 'https://74.249.132:64297' on port '64297'.

Once connected, we are greeted with a dashboard that offers a wide range of tools to help us analyze and manage the data that we collect through our honeypot.
**Tools:** 
- Attack Map: Provides a visual representation of the geographical locations that the attacks originate from, along with other details on the attempted attacks.
- Cockpit: The main dashboard of your honeypot, Cockpit displays information such as number of attacks, the top attackers, and the most frequently targeted services.
- Cyberchef: A powerful tool when it comes to analyzing captured traffic, it allows you to search for and investigate patterns in the data.
- Elasticvue: This elastic search client helps visualize data collected by the honeypot, which can make it easier to interpret large datasets.
- Kibana: This can be used to create custom dashboards and visualize data in various foramts, which enhances your ability to understand and present the attack data.
- Spiderfoot: A reconnaissance tool that performs open-source intelligence gathering, which can provide insights into potential attackers and other related information.

Dashboard
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/c92a42cd47d2ae54c5982bd59e346970.png" style="width: 100%; height: 100%; max-width:50%; " />
</div>
&nbsp;

The Attack Map and Dashboard provide real-time visualizations of attack patterns and honeypot activity.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/6d5019dff2087a91d2158010ae55d7a5.png" style="width: 100%; height: 100%; max-width:60%; " />
</div>
<br>
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/cc0dcd7bb6263e4a996445d4960d692f.png" style="width: 100%; height: 100%; max-width:60%; " />
</div>
<br>
Elasticvue enables detailed data exploration and visualization. Here, we identified a failed login attempt to the admin account.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/e833c77cac8ef4840514cfdabdef464e.png" style="width: 100%; height: 100%; max-width:60%; " />
</div>
<br>
Here we can see Kibana's dashboard catalogue, which will allow us to get into specific data and visualize it easier by using individual dashboards. For example, the T-Pot dashboard displays various graphs and metrics, showcasing the volume and types of attacks
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/30a7fe362b23facfb486fb99e4950a26.png" style="width: 100%; height: 100%; max-width:15%; " />
    <img src="../_resources/85de27d68797b1e57b78b9cb48d44b58.png" style="width: 100%; height: 100%; max-width:55%; " />
</div>
<br>
One cool feature on the T-Pot dashboard is this wordcloud of passwords. The more often each password is used to attempt login, the bigger the password appears here.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/4b70fa826e461a4a44eea348a3a973f1.png" style="width: 100%; height: 100%; max-width:55%; " />
</div>
<br>

Clicking on a source IP of an attack in Kibana will perform a search using Talos Intelligence. This will provide more detailed information about the attackers, which can be useful for further tracking and blocking malicious IPs.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/0a30aaea0334589fc39a76c1b13795a4.png" style="width: 100%; height: 100%; max-width:55%; " />
</div>
<br>



Additionally, the interface includes sections that are dedicated to analyzing different exploits and vulnerabilities. This allows you identify exploits commonly used by attackers, which can help you to further enhance your system's defenses.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/fccf70f84f9f00fa67e1a1ada584a821.png" style="width: 100%; height: 100%; max-width:55%; " />
</div>
<br>



## Spiderfoot:


<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/a3237dec50d3fb8fdfbb234283363762.png" style="width: 100%; height: 100%; max-width:45%; " />
</div>
<br>


With Spiderfoot, you can initiate scans against targets that were detected by your honeypot. We can scan for "All", to reveal comprehensive information about the target, such as its malicious status, DNS records, and associated phone numbers:



Spiderfoot scan results provide extensive information about detected targets.
<div style="display: flex; justify-content: center; gap: 10px; max-width: 75%;">
    <img src="../_resources/36c4cf95f54f502f6970b5f745da4647.png" style="width: 100%; height: 100%; max-width:20%; " />
    <img src="../_resources/912df699da5dc6c872a0f55a8e993cd6.png" style="width: 100%; height: 100%; max-width:35%; " />
</div>
<br>

By understanding and utilizing these tools, you can get a better understanding of the threats that are targeting your network, and take proactive measures to improve your network security posture.


# Conclusion

Over the course of this project, we were able to setup a honeypot using T-Pot on a Microsoft Azure Ubuntu VM to capture and analyze malicious activities. In the steps we took, we were able to successfully configure the VM, install T-Pot, and access its web interface. By leveraging the dashboard tools on T-Pot, such as Attack Map, Cockpit, Cyberchef, Elasticvue, Kibana, and Spiderfoot, we were able to gain valuable insights into attack patterns, exploited vulnerabilies, and details on the attackers.

The web interface that T-Pot provides offers a very comprehensive suite of tools that help us visualize and analyze attack data, which helps to enhance our understanding of the threats that are commonly targeting our network. This setup helps us not only with the collection of critical data regarding our security, but also helps us proactively put in measures to bolster our network's defenses. The use of Spiderfoot can further complement our analysis by scanning and providing detailed information about targets that we detect through the honeypot, which can be used to identify and mitigate potential threats.

The knowledge and techniques acquired from this honeypot implementation will be invaluable for future cybersecurity efforts. I can apply these lessons to improve my ability in anticipating and defending against the everchanging and evolving threats. By leveraging the analyses from these tools, we can better identify the patterns and vulnerabilities, which can assist us in making more informed decisions and robust security strategies. This project helps to underscore the importance of continuous monitoring and adaptation to the threat landscape to maintain a secure network environment.

