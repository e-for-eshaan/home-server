# Building My Home Server with Ubuntu and SSH

## Introduction

I wanted to repurpose my old laptop and turn it into a home server that I could use for various purposes such as hosting websites, storing files, and streaming media. After doing some research, I decided to use Ubuntu as my operating system and SSH (Secure Shell) for remote access to the server. In this document, I will share my experience of building my own home server using Ubuntu and SSH.

## Why Ubuntu and SSH?

I chose Ubuntu because of its reliability, ease of use, and wide community support. Ubuntu is a popular Linux distribution that provides a stable and secure environment for server applications. It also has a user-friendly interface, which made it easier for me to set up and manage my server.

For remote access, I opted for SSH. SSH allows me to securely connect to my server from any location and perform various tasks remotely. It provides encrypted communication, ensuring that my data and login credentials are protected from unauthorized access.

## Setting Up Ubuntu and SSH

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

In this section, I will walk you through my experience of setting up Apache2 and deploying a static React website on my server. The goal was to serve my React website to visitors using the Apache web server and showcase my website to the world.

## Prerequisites

Before getting started, I made sure to have the following:

- A server running Ubuntu with Apache2 already installed. If you haven't set up Apache2 yet, you can refer to the previous section for instructions on how to install it.
- A static React website that I wanted to deploy. If you haven't built your React website yet, you can follow the official React documentation to create a new project and build your website.

## Deploying a Static React Website with Apache2

To deploy my static React website using Apache2, I followed these steps:

1. I built my React website by navigating to the root directory of my React project and running the following command:

```
npm run build
```

This command created an optimized production build of my React website in the \`build\` directory.

2. Next, I copied the contents of the build directory to the default Apache document root directory by running the following command:

```
sudo cp -r build/* /var/www/html/
```

This command copied all the files and directories from the build directory to the default document root directory of Apache2.

3. I configured Apache2 to serve my React website by creating a virtual host file. To create a new virtual host file, I ran the following command:

```
sudo nano /etc/apache2/sites-available/your-website.conf
```

Note: I replaced \`your-website.conf\` with a suitable name for my virtual host configuration file.

4. In the virtual host file, I added the following configuration:


```
<VirtualHost *:80>
ServerName your-domain.com
DocumentRoot /var/www/html
</VirtualHost>
```

I replaced \`your-domain.com\` with my actual domain name or server IP address.

5. I saved the virtual host file and exited the editor.

6. To enable the new virtual host configuration, I ran the following command:

```
sudo a2ensite your-website.conf
```

7. Finally, I restarted Apache2 for the changes to take effect:
```
sudo systemctl restart apache2
```

8. Now, my React website was accessible through the domain name or IP address I specified in the virtual host configuration.

## Conclusion

I successfully set up Apache2 and deployed my static React website on my server. By following the steps outlined in this guide, I was able to showcase my React projects to visitors using a reliable and widely-used web server like Apache2.

To ensure the security of my server and website, I configured appropriate permissions, SSL certificates, and other security measures. Additionally, I made sure to stay up to date with Apache2 and React updates to ensure compatibility and take advantage of new features.

Overall, I am thrilled to share my website with the world and continue exploring the possibilities of web development with React and Apache2.

## References

Here are some resources I found helpful during my journey:

- [Apache HTTP Server Documentation](https://httpd.apache.org/docs/) - Official documentation for Apache HTTP Server.
- [Ubuntu Official Website](https://ubuntu.com/) - Official website of Ubuntu, where you can download the latest version and find documentation.
- [OpenSSH Documentation](https
EOF
