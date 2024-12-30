# Connect to Linux/Ubuntu/RHEL EC2 instance

**Key Pair Creation**

While generating KeyPair, use PPK for putty (Linux only)

<img width="437" alt="image" src="https://github.com/user-attachments/assets/b11665e8-645f-4036-bf38-7c65ccff9d19" />

**Know Error**

**Permissions for Test_Key.pem are too open.**
<img width="946" alt="image" src="https://github.com/user-attachments/assets/dc080ee8-345a-4915-a288-3faa0185d1fb" />

**Solution**

1. Uncheck the Unblock Option -> click Apply and Ok.

  <img width="256" alt="image" src="https://github.com/user-attachments/assets/a4f99678-133b-49f5-9c88-dedb8cd0eb81" />

2. Remove all the permission, expect the login user.
   
  <img width="260" alt="image" src="https://github.com/user-attachments/assets/54064aaf-2625-4358-8598-271f56c9545b" />

**Connecting EC2 from Powershell via SSH**

1. Open Powershell -> Navigate to the path where Key is saved and run the below command.

   ssh -i test_key.pem ubuntu@publicIP

  <img width="626" alt="image" src="https://github.com/user-attachments/assets/323336d8-3695-413f-a0c5-5dd727074331" />
