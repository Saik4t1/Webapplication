# Webapplication

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
6. Access the website using public IP of the instance.
   
   **http://EC2-PublicIP**
   
