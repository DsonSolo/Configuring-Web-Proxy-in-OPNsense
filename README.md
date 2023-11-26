# Configuring Web Proxy in OPNsense
 
In this lab, I successfully configured the Web Proxy in OPNsense within
a multi-LAN virtual environment, aiming to enhance network security and
control web traffic effectively.

**Requirements:**

- Multi LAN Virtual Environment from Lab 3.0

- 2 Windows 10 client PCs

- OPNsense Firewall configured with 2 LAN interfaces

**Step 1: Block Proxy Bypass**

I initiated the configuration by adding a crucial rule to the firewall,
preventing any unauthorized web traffic on the guest network to ensure
proxy bypass prevention. The use of the '**All_Web_Traffic**' alias
streamlined the process, addressing both HTTP and HTTPS traffic without
the need for separate rules.

1.  I navigated to Firewall \> Rules.

2.  Selected 'GuestNetwork'.

3.  Implemented the addition of a new firewall rule by clicking the plus
    sign.

<img src="./media/image1.png" style="width:6.5in;height:1.75in" />

Configuration Details:

- **Action:** Block

- **Protocol:** TCP\UDP

<img src="./media/image2.png"
style="width:5.19097in;height:2.85337in" />

- **Source:** GuestNetwork net

- **Destination Port Range:** All_Web_Traffic

- **Logging:** Enabled

- **Description:** Block Proxy Bypass

> <img src="./media/image3.png"
> style="width:5.65972in;height:4.09967in" />

After configuring the rule, I prioritized its position by moving it to
the top of the list. This ensured the immediate implementation of the
rule, and to solidify the changes.

<img src="./media/image4.png" style="width:6.5in;height:1.31944in" />

I applied them by clicking the arrow on the first rule and executing the
'Apply changes' action.

<img src="./media/image5.png" style="width:6.5in;height:1.56944in" />

This strategic blocking mechanism establishes a robust defense against
potential proxy bypass attempts on the guest network.

**Step 2: Configuring Web Proxy Redirection**

Continuing with the meticulous configuration of the Web Proxy, I
executed the following steps to ensure effective redirection and proxy
management:

I accessed the Opnsense Web Proxy administration panel under "Services
\> Web Proxy \> Administration" and enabled full help for comprehensive
guidance. In the Forward Proxy tab, I selected only "GuestNetwork" as
the proxy interface, ensuring it operates specifically within that
network. To maintain transparency, I enabled the transparent HTTP proxy.

<img src="./media/image6.png" style="width:6.5in;height:3.70833in" />

After configuring these settings, I applied them to make sure they took
effect.

<img src="./media/image7.png"
style="width:3.70788in;height:1.81771in" />

For controlling web traffic on the GuestNetwork, I created a new
firewall rule.

<img src="./media/image8.png"
style="width:6.45833in;height:1.41667in" />

Going into advanced settings, I specified the interface as
"GuestNetwork," the source as "GuestNetwork net," and enabled NAT
Reflection for proper network address translation.

<img src="./media/image9.png"
style="width:4.93229in;height:3.72789in" />

<img src="./media/image10.png"
style="width:5.45313in;height:1.93132in" />

After saving the settings, I applied the changes.

<img src="./media/image11.png" style="width:6.5in;height:0.68056in" />

In the progression of the configuration, I addressed the security of web
traffic by activating SSL inspection. This crucial step ensures that
even encrypted HTTPS traffic is inspected for potential threats or
policy violations. To accommodate this security measure, I added a new
firewall rule, replicating the configuration used for HTTP traffic.

<img src="./media/image12.png"
style="width:4.41146in;height:3.42406in" />

<img src="./media/image9.png"
style="width:4.81138in;height:3.63021in" />

<img src="./media/image10.png"
style="width:5.45313in;height:1.93132in" />

<img src="./media/image11.png" style="width:6.5in;height:0.68056in" />

Ensuring the effectiveness of the configured rules, I meticulously
checked the firewall settings under "Firewall \> Nat \> Port Forward."
This step was crucial to confirm that the rules for port forwarding,
particularly for both HTTP and HTTPS, were successfully implemented. The
verification process adds an extra layer of assurance that the network
is appropriately set up to forward traffic to the proxy, maintaining
security and compliance standards.

<img src="./media/image13.png" style="width:6.5in;height:1.58333in" />

Returning to the Forward Proxy tab, I initiated the process of
establishing a Certificate Authority (CA) by navigating to CA Manager.

<img src="./media/image14.png" style="width:6.5in;height:3.84722in" />

In this step, I added a new CA with the name "Opnsense-SSL" and selected
the method "Create an internal Certificate Authority."

<img src="./media/image15.png" style="width:6.5in;height:1.04167in" />

<img src="./media/image16.png"
style="width:4.89063in;height:2.28072in" />

After providing the necessary Distinguished name information, I saved
the configuration.

<img src="./media/image17.png"
style="width:5.14063in;height:4.11914in" />

Subsequently, I exported the CA certificate and ensured its successful
download.

<img src="./media/image18.png" style="width:6.5in;height:1.27778in" />

<img src="./media/image19.png" style="width:6.5in;height:0.69444in" />

To make this certificate accessible on Guest PC2, I copied and pasted it
onto the desktop. In case standard copy/paste methods were unavailable,
I utilized the drag and drop feature from PC1 to PC2 desktop.

<img src="./media/image20.png"
style="width:5.46354in;height:2.06634in" />

Alternatively, if both copy/paste and drag and drop were non-functional,
I employed the Remote Desktop Protocol (RDP) feature. By opening the
Remote Desktop Connection on PC1 and connecting to PC2 with the
specified IP address (e.g., 192.168.3.10), I facilitated the secure
transfer of the certificate.

<img src="./media/image21.png"
style="width:4.23958in;height:2.66667in" />

The provided credentials, including the username "perscholas" and
password "Ps@12345," ensured successful authentication.

<img src="./media/image22.png" style="width:6.5in;height:3.20833in" />

The next step involved copying the certificate from PC1 (CTRL + C) and
pasting it into the remote computer (PC2) using (CTRL + V).

<img src="./media/image23.png"
style="width:6.3832in;height:4.17188in" />

On PC2, I opened the Opnsense SSL CA folder, clicked on "Install
certificate," and followed the prompted steps.

<img src="./media/image24.png"
style="width:3.41332in;height:3.85938in" />

During installation, I selected "Local Machine" and designated the
Trusted Root Certificate Authorities store for the certificate.

<img src="./media/image25.png"
style="width:3.94271in;height:3.9045in" />

<img src="./media/image26.png"
style="width:5.32662in;height:3.28646in" />

The successful completion of this process was confirmed by the
appearance of the final window. Finally, I clicked "Finish" to conclude
the installation.

<img src="./media/image27.png"
style="width:3.14583in;height:3.09146in" />

Returning to the Forward Proxy tab, I proceeded to configure the
Certificate Authority (CA) for use. Specifically, I selected the
previously created "OPNsense-SSL" CA and applied the changes.

<img src="./media/image28.png"
style="width:5.98958in;height:4.14663in" />

To streamline user access and maintain simplicity, I navigated to the
arrow next to Forward Proxy and accessed Authentication Settings.

<img src="./media/image29.png"
style="width:4.33333in;height:3.17708in" />

Here, I ensured that authentication was disabled by clicking on "Clear
All" for both options and subsequently applying the changes.

<img src="./media/image30.png"
style="width:5.75158in;height:4.38021in" />

Concluding this phase, I activated the proxy by clicking on "Enable" and
applying the changes.

<img src="./media/image31.png" style="width:6.5in;height:1.875in" />

Returning to the Forward Proxy tab, I initiated the setup for web
filtering by accessing Remote Access Control Lists and adding a new
list.

<img src="./media/image32.png"
style="width:6.23438in;height:2.52772in" />

The configurations included enabling the list, providing a URL link for
the UT1 web categorization list, and saving the settings.

<img src="./media/image33.png" style="width:6.5in;height:3.29167in" />

After downloading and applying the Access Control Lists (ACLs), I
navigated to the Edit button, where I selected specific categories for
filtering, such as "bitcoin." Subsequently, I reapplied the ACLs to
implement the chosen categories.

<img src="./media/image34.png" style="width:6.5in;height:2.625in" />

<img src="./media/image35.png"
style="width:4.99479in;height:3.08172in" />

<img src="./media/image36.png"
style="width:5.08309in;height:4.23438in" />

To verify the effectiveness of the web filter, I accessed Guest PC2 and
tested general web traffic by visiting Google, followed by a search for
"bitcoin." Attempting to access coinbase.com, I observed a denial due to
the implemented web filtering.

<img src="./media/image37.png" style="width:6.5in;height:5.43056in" />

<img src="./media/image38.png"
style="width:5.64583in;height:2.17708in" />

<img src="./media/image39.png" style="width:6.5in;height:0.73611in" />

<img src="./media/image40.png" style="width:6.5in;height:1.97222in" />

<img src="./media/image41.png"
style="width:3.76042in;height:3.01042in" />

<img src="./media/image42.png"
style="width:4.86458in;height:5.83333in" />

<img src="./media/image43.png" style="width:6.5in;height:2.68056in" />

<img src="./media/image44.png" style="width:6.5in;height:2.68056in" />

Proceeding to customize the blocklist, I visited the Forward Proxy
settings and accessed the Access Control List.

<img src="./media/image45.png" style="width:6.5in;height:2.15278in" />

I added custom sites like facebook.com and worldstarhiphop.com to the
blacklist, ensuring their successful blocking.

<img src="./media/image46.png" style="width:6.5in;height:5.56944in" />

<img src="./media/image47.png" style="width:6.5in;height:3.29167in" />

<img src="./media/image48.png" style="width:6.5in;height:2.81944in" />

Concluding the project with the caching proxy configuration, I accessed
Services \> Web Proxy \> Administration.

<img src="./media/image49.png" style="width:6.5in;height:2.66667in" />

Navigating to General Proxy Settings and selecting Local Cache Settings,
I configured caching options with considerations for memory cache size
and the enabling of local cache. While demonstrating the caching proxy
setup, it's important to note that caching was enabled for demonstration
purposes only.

<img src="./media/image50.png"
style="width:5.90063in;height:4.44271in" />

This wraps up the detailed configuration of the web proxy in Opnsense,
covering web filtering, testing, custom blocking, and caching proxy
settings.

