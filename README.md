<p align="center">
<img src="https://i.imgur.com/MwrkwEQ.png" alt="DNS Photo"/>
</p>

<h1>Understanding DNS</h1>
This lab hones in on the practical aspects of DNS, a fundamental concept in IT often covered theoretically. The objective is to configure DNS records and observe their functionality in a hands-on environment. Building on a prior lab where I successfully joined a client to my domain, ernestotest.com, I'll be navigating through the lab tasks while logged in as Alain Garcia —an admin account—on both the client and domain controller VMs. It's crucial to be logged in as an administrator for the lab to proceed seamlessly. Let's dive into the practical intricacies of DNS configuration. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>DNS Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/5pjgtVz.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/ha2QGdD.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/jzD1hLa.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
While logged into the client as an admin, let's perform a diagnostic on the command prompt. Pinging "mainframe" currently results in failure. Similarly, using nslookup "mainframe" yields no DNS record. To address this, we'll create a DNS A-record for "mainframe" on the domain controller.

Navigate to the DNS Manager on the domain controller, specifically within the Forward Lookup Zones tab, corresponding to the domain you established (e.g., alaingarciadomain.com). Right-click on the page and initiate the creation of a New Host. Specify the name as "mainframe," and set the IP address identical to the domain controller's to facilitate resolution via ping. Refresh the DNS server to ensure the new record is updated.

Returning to the client, try pinging "mainframe" once more. This time, you should observe successful resolution, confirming the effectiveness of the newly created DNS A-record.
</p>
<br />

<p>
<img src="https://i.imgur.com/OdsLl5x.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/fmh7mlp.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/rpsVpac.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
In the following exercise, we'll explore the DNS cache. On the domain controller, I modified the record address for "mainframe" to 8.8.8.8 (Google) and refreshed the DNS server. Despite this change, when attempting to ping "mainframe" from the client, it still references the old IP address. Running the command ipconfig /displaydns reveals that the DNS cache retains the outdated IP.

To rectify this, we need to clear the cache. The command ipconfig /flushdns will empty the cache. Subsequently, when pinging "mainframe" again, the client-side IP address will be updated to reflect the recent changes. You should observe that the new IP address of the record is now reflected in the ping results.
</p>
<br />

<p>
<img src="https://i.imgur.com/5usVNSm.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/EwVZD3A.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/5kDER7b.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
Now, let's create a CNAME record on the DNS server to direct "search" to Google. Within the DNS Manager's Forward Lookup Zones tab, navigate to the tab corresponding to the domain. Create a new CNAME record named "search" and set it to point to Google. Don't forget to refresh the server to save the changes.

Once this is done, on the client side, attempting to ping "search" and using nslookup will yield the results of the newly created CNAME record, demonstrating the successful resolution of the alias.
<br />

<h2>Lessons Learned </h2>

This lab has provided me with a practical understanding of how DNS functions on both an individual computer and within a network. It illuminated the dynamic nature of DNS records and how changes in these records can impact connectivity. The significance of clearing the DNS cache using the ipconfig /flushdns command became evident as it emerged as a crucial troubleshooting tool.

The initial ping to "mainframe" in this lab showcased the sequence of checks, starting with the DNS cache, then moving on to the host file, and finally consulting the DNS server for resolution. The step-by-step process clarified the mechanics of DNS resolution in a real-world scenario.

Additionally, creating a DNS record and a CNAME record on the DNS server highlighted the versatility of DNS in managing aliases and mapping them to specific IP addresses or domains. This practical experience not only demystified the functionality of DNS but also underscored its critical role in maintaining seamless network communication.






