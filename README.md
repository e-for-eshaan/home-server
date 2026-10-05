# Home Server

An old Lenovo laptop, reborn as an always-on home server. It runs Ubuntu Server, lives on the shelf with the lid closed, and does three jobs: it is reachable from anywhere over SSH, it serves my website over Apache, and it acts as network-attached storage for every device in the house.

![hostnamectl on the server: Ubuntu 22.04.2 LTS on a Lenovo laptop](https://github.com/e-for-eshaan/home-server/assets/76566992/3bbcad2c-8b68-4f72-9f83-c1e526939d37)

## What it does

- **Remote shell.** OpenSSH on a non-default port, so I can administer it from a phone or any laptop without being in the same room.
- **Web hosting.** Apache serves the production build of a React site straight from the box, so a project can go live without paying for hosting.
- **Network storage.** Samba shares a folder to every machine on the LAN. It shows up as a normal network drive on Windows, macOS and Linux, which makes it the house's shared disk for files and media.
- **Costs nothing.** The hardware was already here. A laptop has a built-in battery, a built-in display for emergencies, and idles at a few watts.

## Why Ubuntu and SSH

Ubuntu Server is stable, well documented and has a package for everything I wanted to run. SSH gives an encrypted shell from anywhere, so nothing on the box ever needs a keyboard and monitor plugged in after the first boot.

## Part 1: Ubuntu and SSH

With Ubuntu installed, the first service to bring up is SSH.

1. Update the package index.

   ```
   sudo apt update
   ```

2. Install the OpenSSH server. The service starts on install.

   ```
   sudo apt install openssh-server
   sudo systemctl status ssh
   ```

3. Move SSH off the default port. Open the config, find the `#Port 22` line, uncomment it and pick a new port.

   ```
   sudo nano /etc/ssh/sshd_config
   ```

4. Restart the service so the change takes effect.

   ```
   sudo systemctl restart ssh
   ```

5. Connect from any other machine with `ssh user@<server-ip> -p <port>`. For access from outside the house, forward that port on the router to the server.

## Part 2: Hosting a React site with Apache

The goal here was to put a static React build on the internet from the server itself.

![Apache running on the server](https://github.com/e-for-eshaan/home-server/assets/76566992/65f8cd42-54b4-4e88-b880-2983fe0459ff)

1. Install Apache.

   ```
   sudo apt install apache2
   ```

2. Build the React project on your machine. This produces an optimised `build` directory.

   ```
   npm run build
   ```

3. Copy the build into Apache's document root.

   ```
   sudo cp -r build/* /var/www/html/
   ```

4. Create a virtual host for the site.

   ```
   sudo nano /etc/apache2/sites-available/your-website.conf
   ```

   ```apache
   <VirtualHost *:80>
       ServerName your-domain.com
       DocumentRoot /var/www/html
   </VirtualHost>
   ```

5. Enable the site and restart Apache.

   ```
   sudo a2ensite your-website.conf
   sudo systemctl restart apache2
   ```

The site is now served at the domain or IP in `ServerName`. From here it is the usual hardening: file permissions, a certificate from Let's Encrypt for HTTPS, and keeping Apache and the build up to date.

## Part 3: Network storage with Samba

Samba is what turns the laptop into a NAS. One shared folder, visible to every device on the network.

![Samba's smbd service running on the server](https://github.com/e-for-eshaan/home-server/assets/76566992/e9ca407a-f677-41bc-aa69-4b0f01104afd)

1. Install Samba.

   ```
   sudo apt install samba
   ```

2. Create the folder to share and add a share definition to the end of `/etc/samba/smb.conf`.

   ```
   mkdir -p ~/share
   sudo nano /etc/samba/smb.conf
   ```

   ```ini
   [share]
       path = /home/<user>/share
       browseable = yes
       read only = no
       valid users = <user>
   ```

3. Give the Linux user a Samba password and restart the service.

   ```
   sudo smbpasswd -a <user>
   sudo systemctl restart smbd
   ```

4. Mount it from any client: `\\<server-ip>\share` on Windows, `smb://<server-ip>/share` on macOS and Linux file managers.

## What I learned

- A laptop makes a surprisingly good server: silent, low power, and the battery is a free UPS.
- Putting SSH on a different port keeps the auth log readable. It is not security on its own, but it filters out almost all of the automated noise.
- Apache plus a static build is the simplest possible deploy. There is nothing to keep alive and nothing to crash.

## References

- [Apache HTTP Server documentation](https://httpd.apache.org/docs/)
- [Ubuntu Server](https://ubuntu.com/server)
- [OpenSSH documentation](https://www.openssh.com/manual.html)
- [Samba documentation](https://www.samba.org/samba/docs/)
