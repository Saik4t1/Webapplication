# Host apache site on ubuntu EC2

**Install Apache2 on Ubuntu**

1. Install latest updates on ubuntu.
   
   **sudo apt update**
2. Install Apache2
   
   **sudo apt install apache2 -y**
3. Verify Apache service status
   
   **sudo systemclt status apache2**

   <img width="593" alt="image" src="https://github.com/user-attachments/assets/413e24a5-9aec-4787-bf55-db53c13f1abe" />

4. Start/Stop/Restart Apache service Status

   **sudo systemclt start apache2**
   
   **sudo systemclt stop apache2**

   **sudo systemclt restart apache2**

5. Enable auto start for apache service after boot.

   **sudo systemclt enable apache2**
   
   <img width="647" alt="image" src="https://github.com/user-attachments/assets/c6061842-a1f0-4f5b-a6a3-cc1c31ff1ca4" />

**Configure default Website**

1. Default **index.html** path will be **/var/www/html**.
   
2. Copy webapplication files to Ubuntu.
   
   **scp -i your-key.pem -v /path/to/your-website-files/*** **ubuntu@<instance-public-ip>:/tmp**

3. Now copy the file from tmp folder to /var/www/html/

    **sudo cp /tmp/index.html /var/www/html/index.html**

   **Note:** SUDO is mandatory else it will give permission denied error.
   
5. Restart Apache if required.

   **sudo systemclt restart apache2**

   
**Open Network Ports**
1. For the site to get accessible, we need to Security group to allow HTTP port 80 on Inbound Rule.
   
   **EC2 -> SecurityGroup -> Inbound Rule -> Edit Inbound Rule -> Add HTTP Rule**
    
   <img width="905" alt="image" src="https://github.com/user-attachments/assets/9c9ffee3-f6f5-4b84-b9ed-987676af7e8f" />

2. Access the website using public IP of the instance.
   
   **http://EC2-PublicIP**
   
**Configure Multiple Website on EC2**

We are going to create k3site1.com and k3site2.com on the EC2 instance. Follow below steps to complete the configuration. 

1. Create seperate directory for each websites.
   
   **sudo mkdir -p /var/www/k3site1.com/public_html**

   **sudo mkdir -p /var/www/k3site2.com/public_html**
   <img width="468" alt="image" src="https://github.com/user-attachments/assets/504e3750-9990-45a0-ae43-f353b6f1be20" />

2. Create **index.html** file in each directories.

   <img width="554" alt="image" src="https://github.com/user-attachments/assets/0ccf1b9b-0305-4b1b-b649-1e0da2802599" />

   <img width="707" alt="image" src="https://github.com/user-attachments/assets/32c206da-76fc-4d81-9bf5-9b2ec7d4e6b9" />
   **Note:** Verify the index file content by running cat command. 

4. Create Config file for k3site1.com (Virtual Host File)
   
   <img width="460" alt="image" src="https://github.com/user-attachments/assets/eebb58f9-e51e-472b-a2a9-9ebd4846ae7a" />

    <img width="934" alt="image" src="https://github.com/user-attachments/assets/6545d708-e588-43d2-9642-62fee724cbe7" />

    Paste the config details and press **ctrl+x** and then **Y** and then **Enter**.

   **Sample Configuration:**

   <VirtualHost *:80>
    ServerName k3site1.com
    ServerAlias www.k3site1.com
    DocumentRoot /var/www/k3site1.com/public_html
    ErrorLog /var/www/k3site1.com/error.log
    CustomLog /var/www/k3site1.com/access.log combined
   </VirtualHost>
   
5. Repeate the same step for k3site2.com (Virtual Host File)

   <img width="450" alt="image" src="https://github.com/user-attachments/assets/ee90b1a3-6031-4ac5-b737-4c99be7dfbff" />

   <img width="920" alt="image" src="https://github.com/user-attachments/assets/58f3610d-9427-422a-be49-3ddefae05ed9" />

   Paste the config details and press **ctrl+x** and then **Y** and then **Enter**.

   **Sample Configuration:**

   <VirtualHost *:80>
    ServerName k3site2.com
    ServerAlias www.k3site2.com
    DocumentRoot /var/www/k3site2.com/public_html
    ErrorLog /var/www/k3site2.com/error.log
    CustomLog /var/www/k3site2.com/access.log combined
   </VirtualHost>

6. Now we need to enabled both Virtual host config file.

   **sudo a2ensite k3site1.com.conf**
   
   **sudo a2ensite k3site2.com.conf**

   **sudo systemctl reload apache2**

   <img width="479" alt="image" src="https://github.com/user-attachments/assets/f8bb498f-8ce2-4ed8-9c99-5d7ca0abf344" />
   
7. Now restart Apache service to apply the changes.

   **sudo systemctl restart apache2**
    
   <img width="463" alt="image" src="https://github.com/user-attachments/assets/23ccc31e-efb3-4be4-97d2-77f1a9ae9ef3" />

**DNS Validation:**

1. Update the local host file in client pc.

   <img width="445" alt="image" src="https://github.com/user-attachments/assets/44e43685-627d-4b52-9ca3-b12cb110fc8a" />

   **Sample:**
   
   **PUBLIC_IP k3site1.com www.k3site1.com**
   
   **PUBLIC_IP k3site2.com www.k3site2.com**

   <img width="460" alt="image" src="https://github.com/user-attachments/assets/79d218c2-81ce-443a-908e-fc706e7f4643" />


**Expected Output:**

<img width="670" alt="image" src="https://github.com/user-attachments/assets/fa39c2c1-a8b5-4451-9ef6-0f6eb0377465" />

<img width="644" alt="image" src="https://github.com/user-attachments/assets/c000559f-3a28-403d-af92-c312be87c1db" />
