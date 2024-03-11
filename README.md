-# Hosting-Static-Website-on-EC2-instance-Linux-
Step 1. 
- Create Free Tier AWS Account
- Click on EC2 in AWS Console Page and "Launch Instance"
![Screenshot 2024-02-12 213730](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/88bc1dc7-4a91-4181-83eb-dc3394f8a712)
![Screenshot 2024-02-12 213834](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/afab7f8f-217c-44af-bac1-d49ba7609c3a)
![Screenshot 2024-02-12 213846](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/858e7838-9418-41ec-a453-ba6cbd07cba2)
Step 2.
- Set up the instance type hardware configurations which included, Amazon Linux 64bit x86, Instance type(t2.micro). In Regions where t2.micro is unavailable, you can use a t3.micro instance under the Free Tier.
![Screenshot 2024-02-12 215540](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/b14203cd-b2a0-438f-8387-a5c003b5a838)
![Screenshot 2024-02-12 215607](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/72507872-d176-4571-835a-9dfe7cd8b8e6)
Step 3.
- Created Key Pair to securly connect to Instance
![Screenshot 2024-02-12 215707](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/136b2a1c-f519-43cc-a9e0-41916c3e1217)
- Once the key pair was created, attached key pair to instance
![Screenshot 2024-02-12 215747](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/3bc0a650-c555-4840-b2e2-99f9c7cc3f80)
- Network settings left at default
![Screenshot 2024-03-10 142941](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/f8d7f3c7-ed88-43a4-8fbb-551bb334cb91)
- In red circles I ticked the two options to allow traffic from HTTP and HTTPS in
- Instance launched with 2 checks passed and fully running
![Screenshot 2024-02-12 221502](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/f0a861e4-812b-4908-97f1-cf1b1b88b956)
Step 4.
- Setting a Security Group(essentially a firewall on the cloud) monitors incoming and outgoing traffic)
- I encountered an issue with setting up security group, a VPC (Virtual Private Cloud) was required and this error came up when trying to set up VPC
![Screenshot 2024-02-13 132949](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/867b2e8c-89de-44d2-97bc-43ff44f1eddc)
- This was caused If the date or time is wrong on the local computer, or date/time is wrong for VM/instance, then the credentials will be invalid and we will get “AWS was not able to validate the provided credentials”
- In other words, When the difference between AWS-datetime and your datetime is too big, the credentials will not accepted
- I resolved this by changing the time on my local computer
![Screenshot 2024-02-13 134934](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/3f46f27c-6b79-4de9-8955-ae73f64a0319)
- The diagram below is the correct time:
![Screenshot 2024-02-13 144954](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/7886b34c-9e85-4763-9816-140aa5e20d60)
- This resulted in the VPC being available to be created
![Screenshot 2024-02-13 145411](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/0d46cbde-72e3-4305-a905-08bba0cb9997)
- Next set up a security group as follows:
- Click Security Groups
- Click "Create Security Group"
![Screenshot 2024-02-13 150758](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/2d3934d7-0e67-4370-81de-e4e38f53c03f)
![Screenshot 2024-02-13 150840](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/49d25e14-2d42-4d50-bb1f-9e6f9e455073)
![Screenshot 2024-02-13 150952](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/13777ae4-a131-447f-a021-d29e30c33fd0)
- Create some inbound rules to monitor incoming traffic to only reach my instance
![Screenshot 2024-02-13 151407](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/2858bf10-c34f-4fdc-8f50-06e5eee52966)
- For security reasons, I did not choose Anywhere-IPv4 or Anywhere-IPv6 for Source with a rule for SSH. This would allow access to my instance from all IP addresses on the internet. This is acceptable for a short time in a test environment, but it is unsafe for production environments
- For Outbound rules, keep the default rule, which allows all outbound traffic
![Screenshot 2024-02-13 151724](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/6e330807-e6c5-4c17-a756-6df907ea50fb)
- I now created the security group as follows:
- Click create security group
  ![Screenshot 2024-02-13 151811](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/7e38598c-7ecb-4c7e-8353-bab4c1aa99c2)
  ![Screenshot 2024-02-13 151921](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/c2664c5d-7493-4552-b822-be3d46bc9702)
Step 5.
Connect to Linux Instance
- To prepare to connect to an instance, I got the following information from the Amazon EC2 console:
- The Public IPv4 DNS. I will use this IP to access the EC2 instance
- The Purpose of this allows us to be able to connect to our instance and send files to and from the local computer and the instance
- The Instance ID
![Screenshot 2024-02-14 142136](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/dca0def3-ae6e-4333-b6d6-c12098360e75)
- If no Public IPv4 Dns name is showing, ensure the instance status is running
![Screenshot 2024-02-14 145016](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/f37e41d6-9272-4d65-9269-68583bf8b55c)
- Now I connected the instance
![Screenshot 2024-03-11 142758](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/59440a22-2e03-4b6a-895b-4a20052bf2e6)
- I used the EC2 Instance Connect Method to connect the instance
![Screenshot 2024-02-14 145440](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/17166f9b-1a88-4972-ac6d-e25cc0d32ef7)
- This is the conclusion from connecting the instance
![Screenshot 2024-02-14 145610](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/3ca4a555-9024-4d87-a7e7-cde6844fbd67)
- Initially, when creating the EC2 instance, the key pair was stored in my local computer which is important to locate as it allows a user to be identified to have access to the instance
Step 5.
- I installed an Apache web server with PHP and MySQL support on my Amazon Linux instance (sometimes called a LAMP web server or LAMP stack). I will use this server to host a static website that reads and writes information to a database
- Before proceeding I had to make sure I had the correct security group inbound configurations which entailed SSH (port 22), HTTP (port 80), and HTTPS (port 443) connections. This controlled traffic coming into the instance
![Screenshot 2024-02-16 000120](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/65adc236-520e-4909-ad9b-99d0041e1ede)
- Once I configured the security group, I connected to my instance and did a quick software update to make sure I had the correct packages, latest security updates, and bug fixes. To do this I typed in “sudo yum update -y” in the Linux interface beside [ec2-user ~]$.
- I came across an issue with the instance not connecting with this error message
![Screenshot 2024-02-16 010401](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/4579c462-3c47-4361-960e-1ea76650c776)
- I resolved this by configuring the security group settings and changing the source of SSH from “My IP” to “anywhere IPv4” which resolved this issue allowing a connection to the instance
![Screenshot 2024-02-16 010317](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/189cf42e-e388-4eec-b7ea-35ad156ae182)
- Now continuing with the update as stated before the issue. This was the conclusion from the update
![Screenshot 2024-02-16 010802](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/204d72cc-b66a-451e-9e2d-065f2e5e35f8)
- Now that the instance is current, I installed the Apache web server, MySQL, and PHP software packages
![Screenshot 2024-02-16 125441](https://github.com/AllenUdejiole/Hosting-Static-Website-on-EC2-instance-Linux-/assets/160611100/9e04cd4e-710c-4434-9ffa-1f0c885d3491)


