# AWS Workspaces Lab
A self-paced lab for setting up AWS Workspaces
  
### Setup:
- Download [workspaces.cf.json](https://github.com/mjuliana/AWSWorkspacesLab/blob/master/workspaces.cf.json)
 from GitHub
- In the AWS console navigate to *CloudFormation*
- Click **Create Stack**
- Under *Prepare template* select *Template is ready*
- Under *Template source* select *Upload a template file*
- Select *Choose file* and upload workspaces.cf.json which you donwloaded earlier
- Click **Next**
  - **Note:** This template creates a VPC with a 10.0.0.0/16 CIDR block. If your exsisting account already has a VPC in that range you can update the VPC and subnet ranges in the template in order to avoid an error.
- Under *Stack name* type *WorkSpaceVPC*
- On the *Configure stack options* page you can leave the defaults
- On the *Review WorkSpaceVPC* page Click **Create Stack**

TODO: [ ] Add initial architecture diagram of what the tempalte creates

### Create a WorkSpace:
- Once the CloudFormation stack is complete navigate to *Directory Service* 
- In the navigation pane select *Directories*
- Click on the Directory ID of the directory named workspaces.example.com
- On the *Directory details* page scroll down to the *AWS apps & services* section
- Click on **Amazon WorkSpaces**
- On the *Workspaces Directories* page select the directory named workspaces.example.com
- Click on the **Actions** dropdown and select *Register*
- On the *Select Subnets* section for 
  - *Subnet 1* select the 10.0.1.0/24 subnet
  - *Subnet 2* select the 10.0.2.0/24 subnet
- Under the *Configurations* section for
  - *Enable Self Service Permissions* select **No**
  - *Enable Amazon WorkDocs* select **No**
- Click **Register**
- On the Directories page the directory will show *REGISTERING* under the Registered column
  - Click on the refresh icon to check when it shows registered
- Once the directory is registered select *WorkSpaces* in the navigation page
- On the *WorkSpaces* page click **Launch WorkSpaces**
- Under the *Select a Directory* section select workspaces.example.com as the directory
- Click **Next Step**
- On the *Identify Users* page go to the *Create New Users and Add Them to Directory* section and enter values for:
  - Username
  - First Name
  - Last Name
  - Email (this is an email you can access)
- Click **Create Users**
- Scroll to the bottom and click *Next Step*
- On the *Select Bundle* page select the *Value with Windows 10* bundle
- Scroll to the bottom and click **Next Step**
- In the *Running Mode* section on the *WorkSpaces Configuration* page select *AutoStop* and set the *AutoStop Time (hours)* to 1
- Leave the rest of the default settings
- Scroll to the bottom and click **Next Step**
- On the *Review & Launch WorkSpaces* page scroll to the botton and click **Launch WorkSpaces**
- On the *WorkSpaces* page the provisioning WorkSpace will be in a status of *PENDING*
  - The WorkSpace can take up to 20 minutes to provison
- Once provisioned you will receive and email and the status of the WorkSpace will change to *AVAILABLE*

### Access a WorkSpace:
- In the email you receive click on the link that says *Complete your user profile and download a WorkSpaces client*
- Set your WorkSpace credentials
  - Verify the prefilled data and then set a password
- Download the appropriate WorkSpaces desktop client
- Launch the client and enter the registration code that was in the email
-  Click **Register**
-  Enter you WorkSpace credentials and click **Sign In**
-  You're now signed in to your WorkSpace!

### Adding Applications:
- In the AWS console navigate to *WorkSpaces*
- In the navigation pane under *Application Manager* select *Applications*
- Click **Get started building your catalog**
- On the *Select subscription plan* page select *WAM Lite*
- Scroll to the bottom and click **Confirm**
- On the *Add applications to catalog from AWS Marketplace* page search for Putty
- In the results click *PuTTY*
- On the *PuTTY* page scroll down and click **Accept terms and subscribe**
- On the *Add applications to catalog from AWS Marketplace* click **Return to application catalog**
- On the *Applications* page change *Source* to *AWS Marketplace*
- Select *PuTTY*
- Click **Actions** and select **Assign application(s) to users**
- On the *Select users* screen select the workspaces.example.com directory
- For *Type* select *Users*
- Type your username and click **Search**
- In the search result select your username and click the **>** button to add your username to the *Selected users and groups* list
- Select your username from the *Selected users and groups* list
- Click **Next**
- On the *Configure options* page click **Review**
- Review the changes
- Click **Confirm and assign**
- Go back to your WorkSpace via the desktop client
- Choose the Amazon WAM shortcut on the desktop of your WorkSpace
  - If there is no Amazon WAM shortcut on the desktop [follow these instructions](https://github.com/mjuliana/AWSWorkspacesLab/blob/master/wam_setup.md)
- In *WorkSpaces Application Manager* the *MY APPS* section shows the applications that have been assigned to you and are already installed
- In *WorkSpaces Application Manager* click **Discover** 
- On PuTTY click the triangle to install
- Once installed you should see a checkmark on PuTTY
- You can now launch PuTTY by clicking the arrow on PuTTY on the *WorkSpaces Application Manager* or via the Windows Start menu

### Remove Applications:
- In the AWS console navigate to *WorkSpaces*
- In the navigation pane under *Application Manager* select *Applications*
- Change *Source* to *AWS Marketplace*
- Click on *PuTTY*
- On the PuTTY detail page scroll down and expand the *Users and Groups* section
- Select your username from the list and click **Remove user or group**
- On the warning message click **Continue**
- Go back to your WorkSpace via the desktop client
- Choose the Amazon WAM shortcut on the desktop of your WorkSpace
  - PuTTY should now be gone from WAM and the Windows start menu

### Clean Up:
- In order to be able to remove the directory that was set up with the CloudFormation script you need to disconnect WorkSpaces and WorkSpaces Appliction Manager for the directory
- In the AWS console navigate to *WorkSpaces*
- In the navigation pane under *Application Manager* select *Usage*
- On the *Usage* page select the *Users* tab
- Select the workspaces.example.com directory from the *Directory* drop-down
- Click **Remove all assignments**
- Type REMOVE in the conformation box
- Click **Remove all assigments**
  - **Note:** This action can take up to 10 minutes to complete but you can continue with the next steps
- In the navigation pane under *WorkSpaces* select *WorkSpaces*
- Select all WorkSpaces (in case you launched more)
- Click on the **Actions** dropdown and select **Remove workspaces**
- On the warning message click **Remove**
- The status will change to TERMINATING
  - **Note:** This action can take up to 5 minutes to complete. 
- In the navigation pane under *WorkSpaces* select *Directories*
- Select the workspaces.example.com directory
- Click on the **Actions** dropdown and select **Deregister**
- On the warning message click **Deregister**
  - The directory should now say No under *Registered*
- In the AWS console navigate to CloudFormation
- Select the *WorkSpacesVPC* stack and click **Delete**
- On the warning box click **Delete stack**
- This will take several minutes to complete but when it is done your account should to cleanup up!

