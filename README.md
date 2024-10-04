# Web Deployment Script - README.md

This repository contains two scripts used for deploying a web application to remote servers.

1. webdeploy.sh

This script automates the deployment process across multiple servers listed in a separate file named remhosts. The script performs the following actions:

Connects to each server in the remhosts file.
Pushes the multios_websetup.sh script to the /tmp directory on the remote server.
Executes the multios_websetup.sh script with sudo privileges on the remote server.
Removes the multios_websetup.sh script from the remote server's /tmp directory.


2. multios_websetup.sh

This script handles the actual deployment tasks on the remote server. It includes logic to determine the operating system (CentOS or Ubuntu) and install the appropriate dependencies (httpd and wget for CentOS, apache2 and wget for Ubuntu). It then performs the following actions:

Downloads the web application archive (2098_health.zip) from a specified URL.
Extracts the downloaded archive to a temporary directory (/tmp/webfiles).
Copies the extracted files from the temporary directory to the web server's document root (/var/www/html).
Restarts the web server service (httpd on CentOS, apache2 on Ubuntu).
Removes the temporary directory.
Displays the status of the web server service and lists the contents of the document root directory.
Requirements:

Server access with sudo privileges for the user specified in the webdeploy.sh script (default: devops).
ssh access to the remote servers listed in the remhosts file.
How to Use:

Edit the remhosts file and add the hostnames of the servers you want to deploy to.
(Optional) Modify the URL variable in multios_websetup.sh to point to a different web application archive.
Make sure the webdeploy.sh script has execute permissions (chmod +x webdeploy.sh).
Run the webdeploy.sh script to initiate the deployment process on all servers listed in remhosts.
Note:

This script redirects the output of package installation commands (yum install and apt update) to /dev/null to avoid cluttering the console output.
Consider adding error handling and logging mechanisms to the scripts for a more robust deployment process.