
# Compute Engines

![arch](./pics/gcp_computing_architectures.png)



## Lab
### 1. Use Cloud Marketplace to deploy a LAMP stack
1. In the Google Cloud Console, on the Navigation menu (Navigation menu icon), click Marketplace.

2. In the search bar, type LAMP and then press ENTER.

3. In the search results, click LAMP Packaged by Bitnami.

    - If you choose another LAMP stack, such as the Google Click to Deploy offering, the lab instructions will not work as expected.

4. On the LAMP page, click Launch.

    - If this is your first time using Compute Engine, the Compute Engine API must be initialized before you can continue.

5. For Zone, select the deployment zone that Qwiklabs assigned to you.

6. For Machine Type, select E2 as the Series and e2-medium as the Machine Type.

7. Leave the remaining settings as their defaults.

8. Accept the Google Cloud Marketplace Terms of Service near the bottom of the page.

9. Click Deploy.

10. If a Welcome to Deployment Manager message appears, click Close to dismiss it.

    - The status of the deployment appears in the console window: lampstack-1 is being deployed. When the deployment of the infrastructure is complete, the status changes to lampstack-1 has been deployed.
    - After the software is installed, a summary of the details for the instance, including the site address, is displayed.

### 2. Verify your deployment
1. When the deployment is complete, click the Site address link in the right pane. (If the website is not responding, wait 30 seconds and try again.) If you see a redirection notice, click on that link to view your new site. 
   - Alternatively, you can click Visit the site in the Get started with LAMP Packaged by Bitnami section of the page. A new browser tab displays a congratulations message. This page confirms that, as part of the LAMP stack, the Apache HTTP Server is running.

2. Close the congratulations browser tab.

3. On the Google Cloud Console, under Get started with LAMP Packaged by Bitnami, click SSH. => In a new window, a secure login shell session on your virtual machine appears.

4. In the SSH window, to change the current working directory to /opt/bitnami, execute the following command: `cd /opt/bitnami`

5. To copy the phpinfo.php script from the installation directory to a publicly accessible location under the web server document root, execute the following command:

    `sudo sh -c 'echo "<?php phpinfo(); ?>" > apache2/htdocs/phpinfo.php'`

    - The phpinfo.php script displays your PHP configuration. It is often used to verify a new PHP installation.

6. To close the SSH window, execute the following command:

    `exit`

7. Open a new browser tab.

8. Enter the following URL, and replace `SITE_ADDRESS` with the URL in the Site address field in the right pane of the lampstack page.

    `http://SITE_ADDRESS/phpinfo.php`

    - A summary of the PHP configuration of your server is displayed.
    - Note: If you can't see the web page in the browser on your corporate laptop: If possible, exit any corporate VPN/network and try again. Enter the IP address on another device, such as a tablet or even a phone.
9. Close the phpinfo tab.

 # Lab
 eu
 ingress: 10.210.0.2
 `ping -c 3 10.210.0.2`
 external IP: 34.17.48.241
 `ping -c 3 34.17.48.241`

 # Lab
 internal IP: 10.180.0.2
 external IP: 34.106.111.0

 blogdb MYSQL ungeTat394@@36
 pub ip: 34.72.215.183

 blogdbuser ungeTat#44

 # Lab
 project id : qwiklabs-gcp-00-cc51afe9eca9
## Confirm that needed APIs are enabled
Kubernetes Engine API
Container Registry API
## Start a Kubernetes Engine cluster
 `export MY_ZONE="us-west1-c"`
 `gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2` => Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes
 `kubectl version`

 ## Run and deploy a container
 `kubectl create deploy nginx --image=nginx:1.17.10`
 `kubectl get pods`
 `kubectl expose deployment nginx --port 80 --type LoadBalancer`
 `kubectl get services` => get external IP of the nginx
 `kubectl scale deployment nginx --replicas 3` => scale up 