# gcp - Deployment Manager

Google Cloud Marketplace lets you quickly deploy functional software packages by providing pre-defined templates with Deployment manager



# gcp - jenkin box set up 

1. Navigate to Marketplace
   1. In the Google Cloud console, in the Navigation menu (Navigation menu icon), click __Marketplace__.
   2. Locate the Jenkins deployment by __searching__ for `Bitnami package for Jenkins`.
   3. Click on the deployment and read about the service provided by the software. 
      1. Jenkins is an __open-source continuous integration__ environment. 
      2. You can define jobs in Jenkins that can perform tasks __such as running a scheduled build of software and backing up data__.
      3. Notice the __software that is installed as part of Jenkins__ shown in the left side of the description.
2. Launch Jenkins
   1. Click __Get Started__.
   2. Verify the deployment, accept the terms and services and click __Agree__.
   3. For the popup `Successfully agreed to terms` click __Deploy__.
   4. If prompted, click on __Enable__ for the `Compute Engine API` and the `Infrastructure Manager API`.
   5. On the Deployment page, under Deployment Service Account, __select Existing Account and choose the account Compute Engine default service account `serviceAccount:<project-id>-compute@developer.gserviceaccount.com`__.
   6. Select zone.
   7. For __Machine Type, select E2__ as the Series and e2-standard-2 (2 vCPU, 1 core, 8GB memory) as the Machine Type.
   8. Leave everything as default and click Deploy.
3. Examine the deployment
   1. Details tab -> note the admin user and password
   2. Details tab -> Site URL -> login
4. Admin
   1. From the Navigation menu navigate to Compute Engine > VM instance.
   2. Click your jenkins instance
   3. Click SSH to connect to the Jenkins server.
      1. The console interface is performing several tasks for you transparently. For example, it has transferred keys to the virtual machine that is hosting the Jenkins software so that you can connect securely to the machine using SSH.
   4. stop and restart
    ```shell
    sudo /opt/bitnami/ctlscript.sh stop
    sudo /opt/bitnami/ctlscript.sh restart
    ```
   5. `exit` to close the shell 
