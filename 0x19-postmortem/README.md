**#0x19-postmortem task using webtack debugging #1**



>**Issue Summary**

Duration of the outage: The outage started at 13:00PM and was resolved around 14:50PM Central African Time




>**Impact:**

Firewalls on the host machine were blocking incoming connections on port 80




>**Root Cause:**
>
Incorrectly configured firewall settings inadvertently restricted access to port 80, preventing web traffic from reaching the server




>**Timeline:**
>
13:00 PM: The issue was detected by the ALX(Platform) attempted to access the website and found it unresponsive

13:10 PM: ALX monitoring alerts indicated that the site was down, and the team.

13:15 PM: The investigation focused on ensuring port 80 is not reserved for router management and changed the management port.

13:27 PM: Investigation led to verifying internal IP Addres to confirm that the port forwarding rule points to the correct internal IP address of the web server.

13:42 PM: Rules were modified to prevent blocking the port to ensure that the host firewall allows incoming traffic on port 80. 

13:50 PM: The issue was resolved, and the site was back online.




>**Root Cause and Resolution**

>**Root Cause:**
>
Misconfigured port forwarding rules, such as incorrect internal IP addresses or protocols resulted in port 80 not being properly mapped to the intended device.

>**Resolution:**
>
The port forwarding rule to point to the correct internal IP address was updated.The team made sure that the incoming traffic on port 80 is allowed.




>**Correcteive and Preventive Measures**

>**Improvements:**
>
Maintaining a record of the network settings, including port forwarding rules and firewall configurations, for easier troubleshooting in the future. Use network monitoring tools to detect unauthorized access attempts or issues with port usage earlier.




>**Task List:**

Create and execute script link sites available configuration to sites-enabled after each configuration change. Add a monitoring check to ensure that Nginx is correctly listening on port 80.



>**Example Script**

Here is the script I menrioned to ensure the configuration is always active:
[bash](Copy code) #!/usr/bin/env bash


>**Ensure Nginx is properly configured and listening on port 80**

cat/etc/nginx/sites-available/default>/etc/nginx/sites-enabled/default sudo service nginx restart



>**This ensures that the correct configuration is enabled and restarts Nginx to apply changes**
>

**Flow diagram**
![Screenshot_20240921_162442_Perplexity](https://github.com/user-attachments/assets/8be85c4b-f509-4459-b2b3-6ad8624172ae)


**Postmortem**
![images (7)](https://github.com/user-attachments/assets/dc993a80-8e8f-42f5-a419-371457f575a2)


