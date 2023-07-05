# Building a Home Server with Ubuntu and SSH

![home-server](https://example.com/home-server-image.png)
<br/>
###### *Fig 1. A visual representation of a home server setup.*

## Introduction

This blog post will guide you through the process of setting up a home server using your old laptop and Ubuntu operating system. We will use SSH (Secure Shell) for remote access to the server. By following this guide, you'll be able to create your own personal server that can be used for various purposes, such as hosting websites, file storage, media streaming, and more.

## Prerequisites

Before getting started, make sure you have the following:

- An old laptop or computer that you want to repurpose as a home server.
- Ubuntu operating system installed on your laptop. You can download the latest version of Ubuntu from the official website and install it following the instructions provided.
- Basic knowledge of the Linux command line.

## Setting up SSH Server

## Setting Up a Static IP for Ubuntu Desktop

In a typical network setup, devices are assigned dynamic IP addresses by a DHCP server. This dynamic IP assignment works well for most situations. However, there are cases where having a static IP address for your Ubuntu Desktop can be beneficial.

A static IP address is a fixed IP that you manually assign to your computer instead of relying on automatic assignment. Here's how you can set up a static IP for your Ubuntu Desktop:

1. Open a terminal on your Ubuntu Desktop.

2. Edit the network configuration file using the following command:
   ```bash
   sudo nano /etc/netplan/01-netcfg.yaml
   ```

SSH allows secure remote access to your server. To set up SSH on your Ubuntu home server, follow these steps:

1. Open a terminal on your Ubuntu machine.

2. Update the package lists on your system by running the following command:
   ```
   sudo apt update
   ```

3. Install the OpenSSH server package by running the following command:
   ```
   sudo apt install openssh-server
   ```

4. Once the installation is complete, the SSH service will start automatically. You can verify the status of the SSH service by running the following command:
   ```
   sudo systemctl status ssh
   ```

   If the service is active and running, you should see a message indicating that the SSH service is active.

5. By default, SSH runs on port 22. If you want to change the default port for added security, you can edit the SSH configuration file by running the following command:
   ```
   sudo nano /etc/ssh/sshd_config
   ```

   Locate the line that specifies the port (usually \`#Port 22\`) and remove the \`#\` symbol. Change the port number to your desired value, save the file, and exit the editor.

6. If you made any changes to the SSH configuration file, you need to restart the SSH service for the changes to take effect. Run the following command to restart the SSH service:
   ```
   sudo systemctl restart ssh
   ```

7. Your home server is now set up with SSH. You can access it remotely using an SSH client by connecting to the IP address of your server and the port number you specified (default is 22).

## Conclusion

Congratulations! You have successfully set up a home server using your old laptop and Ubuntu. With SSH enabled, you can now securely access your server remotely and perform various tasks. This opens up a world of possibilities for hosting websites, storing files, running applications, and more, all within the comfort of your own home.

Remember to keep your server's security in mind by using strong passwords, configuring firewall settings, and keeping your system up to date with security patches.

If you want to explore more advanced server configurations and applications, there are numerous resources available online to help you dive deeper into the world of home servers and Linux administration.

Happy server building and happy exploring!

# Deploying a Static React Website with Apache2

![apache2-react](https://example.com/apache2-react-image.png)
<br/>
###### *Fig 1. Illustration of deploying a static React website with Apache2.*

## Introduction

This blog post will guide you through the process of setting up Apache2 and deploying a static React website on your server. By following this guide, you'll be able to serve your React website to visitors using the Apache web server, enabling you to showcase your website to the world.

## Prerequisites

Before getting started, make sure you have the following:

- A server running Ubuntu with Apache2 already installed. If you haven't set up Apache2 yet, you can refer to the previous section for instructions on how to install it.
- A static React website that you want to deploy. If you haven't built your React website yet, you can follow the official React documentation to create a new project and build your website.

## Deploying a Static React Website with Apache2

To deploy your static React website using Apache2, follow these steps:

1. Build your React website by navigating to the root directory of your React project and running the following command:
   ```
   npm run build
   ```
   This command will create an optimized production build of your React website in the \`build\` directory.

2. Copy the contents of the build directory to the default Apache document root directory by running the following command:
   ```
   sudo cp -r build/* /var/www/html/
   ```
   This command copies all the files and directories from the build directory to the default document root directory of Apache2.

3. Configure Apache2 to serve your React website by creating a virtual host file. Run the following command to create a new virtual host file:
   ```
   sudo nano /etc/apache2/sites-available/your-website.conf
   ```
   Replace \`your-website.conf\` with a suitable name for your virtual host configuration file.

4. In the virtual host file, add the following configuration:
   ```
   <VirtualHost *:80>
       ServerName your-domain.com
       DocumentRoot /var/www/html
   </VirtualHost>
   ```
   Replace \`your-domain.com\` with your actual domain name or server IP address.

5. Save the virtual host file and exit the editor.

6. Enable the new virtual host configuration by running the following command:
   ```
   sudo a2ensite your-website.conf
   ```

7. Restart Apache2 for the changes to take effect:
   ```
   sudo systemctl restart apache2
   ```

8. Your React website should now be accessible through the domain name or IP address you specified in the virtual host configuration.

## Conclusion

Congratulations! You have successfully set up Apache2 and deployed your static React website on your server. By following the steps outlined in this guide, you can showcase your React projects to visitors using a reliable and widely-used web server.

Remember to keep your server and website secure by configuring appropriate permissions, SSL certificates, and other security measures. Additionally, stay up to date with Apache2 and React updates to ensure compatibility and take advantage of new features.

Now you can share your website with the world and continue exploring the possibilities of web development with React and Apache2.

## References

Here are some resources for further reading:

- [Apache HTTP Server Documentation](https://httpd.apache.org/docs/) - Official documentation for Apache HTTP Server.
- [Ubuntu Official Website](https://ubuntu.com/) - Official website of Ubuntu, where you can download the latest version and find documentation.
- [OpenSSH Documentation](https
