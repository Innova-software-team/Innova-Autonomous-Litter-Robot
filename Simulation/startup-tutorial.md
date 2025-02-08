# Getting started
## Setting up a local VM
If you have a decent computer, and you'd prefer to have things stored locally, you can set up the VM on your computer.
 - First download any virtual machine software, such as VirtualBox, and create a new virtual machine by mounting the image we provide [here](https://storage.cloud.google.com/amaso-bucket-0/robotics-development-vm-v1.vmdk)
 - If you don't know how to do this, you should be able to find a tutorial for using a vmdk file with whatever software you're using.
 - If you choose this approach, you don't need to do the rest of the setup.

## Setting up your cloud vm
### Create google cloud account
 - Go to [cloud.google.com](https://cloud.google.com)
 - Click "Start free" and setup your account. Your account will be initialised with $300 free credit for 3 months.
 - Create a project

### Accessing the VM Image and creating an virtual machine instance
 - [go to cloud compute](https://console.cloud.google.com/compute/instances)
 - Open the google cloud shell by cluicking an item near the top right of the screen.
 - Complete any setup for google cloud shell if required
 - ```gcloud compute images list --project strange-calling-290115 | grep -i robotics```. This should show you the available disk images you can use to create a VM with the software you need.
 - Next, you will create a VM using the provided disk image. You can name it anything, but anything along the lines of 'robotics-vm' works. You can get your project id by clicking your project name in the top left corner, and it should show up.
 - ```gcloud compute instances create [Name of instance you are creating] --image robotics-development-vm-v1 --image-project strange-calling-290115 --project [YOUR_PROJECT_ID]```

### Making the VM accessible
 - In order to log into your VM remotely using SSH, you will need to generate a keypair for encryption, then give the VM your public key
 - Open a command prompt or terminal:
   - If Unix:
     - ```ssh-keygen -C [DESIRED_USERNAME] -f [PATH]``` : if unsure about where to set PATH, ~/.ssh/VM-access-key
     - ```cat [PATH].pub```
   - 
   - If Windows:
     - ```IDK I CBA RN```
     - ```type [PATH].pub```
 - Copy the output, which should be the public key.
 - On the instances page, click on the name of the instance you created > edit > ssh-keys > new key.
 - paste the public key into the box, and save the changes.

### Connecting
 - [go to cloud compute](https://console.cloud.google.com/compute/instances)
 - If the VM instance isn't already running, start it.
 - Copy the external ip of the instance
 - Open a terminal/cmd prompt
 - ```ssh [DESIRED_USERNAME]@[EXTERNAL_IP] -i [PATH]```, where PATH is the path of the key you generated earlier.

### Setting up chrome remote desktop for access to GUI. 
 - In order to access the desktop environment with GUI from any computer, you must link your google account and start the chrome remote desktop service.
 - [remote desktop setup](https://remotedesktop.google.com/headless)
 - Click a few buttons, then you should see 3 commands. Copy the one for Debian Linux, and paste it into the terminal which should currently be connected to the VM via ssh.
 - The command should look similar to: ```DISPLAY= /opt/google/chrome-remote-desktop/start-host --code="_____" --redirect-url="https://remotedesktop.google.com/_/oauthredirect" --name=$(hostname)```
 - After running the command, if all went well, you should be able to [access the VM]("https://remotedesktop.google.com/access")
 - If it was successful, you can now disconnect from ssh, using ```exit```
