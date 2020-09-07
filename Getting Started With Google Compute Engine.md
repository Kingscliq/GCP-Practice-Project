# LAB: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives
    In this lab, you will learn how to perform the following tasks:

        -Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

        -Create a Compute Engine virtual machine using the gcloud command-line interface.

        -Connect between the two instances.

## Steps:
1. Create a Compute Engine Virtual Machine a virtual machine using the GCP Console

    gcloud compute instances create my-vm-1 --machine-type 'n1-standard-1' --image-project 'debian-cloud' --image 'debian-9-stretch-v20190213' --subnet 'default' --tags http

    gcloud compute firewall-rules create allow-http --action=ALLOW --destination=INGRESS --rules=http:80 --target-tags=http



2. Create a virtual machine using the gcloud command line interface

    -choose a from the output of this zones and use the greg command to filter the result to list the zones associated  with the US central 1

            gcloud compute zones list | grep us-central1


    -set the default zone to the one you chose
    
            gcloud config set compute/zone us-centerl1-b
    
    -create a VM instance called my-vm-2 in that zone
        
            gcloud compute instances create my-vm-2 --machine-type 'n1-standard-1' --image-project 'debian-cloud' --image 'debian-9-stretch-v20190213' --subnet 'default' --tags http



3. Connect Between the two vm instances

        -Connect to my-vm-2:

                gcloud compute ssh my-vm-2

        - Ping my-vm-1 from my-vm-2 four times using this command:

                ping -c 4 my-vm-1
        
        - Use the ssh command to open a command prompt on my-vm-1:

                ssh my-vm-1

        - Use the command to install the Nginx web server on my-vm-1:

                sudo apt-get install nginx-light -y
        
        - Use the nano text editor to add a custom message to the home page of the web server (Note: the command is for Linux Users):

                sudo nano /var/www/html/index.nginx-debian.html

        - Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

                Hi from Kingsley

        - Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.


        - Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

                curl http://localhost/

                Result: The response will be the HTML source of the web server's home page, including your line of custom text.

        - To exit the command prompt on my-vm-1, execute this command:
                
                exit

        - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

                curl http://my-vm-1/
        
                Result: The response will again be the HTML source of the web server's home page, including your line of custom text.


        - Get the external IP address of my-vm-1 instance from this command

                gcloud compute intances list --zone us-central1-a

        - Paste the copied IP address of my-vm-1 into a new tab of the browser and hit the enter key on the keyboard

            Result: You will see your web server's home page, including your custom text.ex565





