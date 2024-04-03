**Hello!**

This is a tutorial for installing and running nginx servers by Jaymond.
This is a full guide to installing and running nginx servers on an ArchLinuxcomputer. Before installing or configuring any file, make sure your Linux isup to date. You can update your linux using the following command:

    `sudo pacman -Syu`

Once your Linux is up to date, we can start by installing all our necessary softwares.

**Installing Vim**

Vim is essential for editing configuration files in Nginx. It's a widely used text editor on Linux systems. Install Vim by executing the following command:

    `sudo pacman -S vim`

This command installs Vim, enabling you to edit files effectively. With Vim ready, let's move on to installing Nginx.

**Installing Nginx**

Installing Nginx is as straightforward as Vim. Execute the following command to install Nginx:

    `sudo pacman -S nginx`

Now that nginx is installed, let's try and see if it works. Use the following command to start an nginx server:

    `sudo systemctl start nginx`

The _systemctl_ command is used to control and manage system services. By issuing _sudo systemctl start_, we instruct Linux to initiate a process on our system—in this case, Nginx.

Now, our nginx should be active. In order to check, use the following line of code:

    `sudo systemctl status nginx`

Similar to our last command, this command tells Linux to check the status ofactive processes, this one being nginx.

This command should return a list of information regarding nginx, but the
one we are interested in is _Active_. This will, of course, tell us if nginxis currently active. If _Active_ returns _active_ in green, that means nginx is active and everything is good. However, if _Active_ returns _failed_ in red, nginx is not running. Please ensure the start code does not have typos.

In order to stop nginx from running, run the following code:

    `sudo systemctl stop nginx`

**Nginx Configuration**

Now that nginx can properly run, we can configure our server to host our owndata.

Configuration files for Nginx are typically found in the /etc/nginx directory. To begin editing these configurations, use:

    `sudo vim /etc/nginx/nginx.conf`

After using this command, you will find yourself in a long text file with all of nginx's configurations.

Before we change any nginx configurations, it is important to understand how this configuration file works. Upon opening _nginx.conf_, you will find two blocks:

```
	events {
	}

	http {
	}
```

Of course, these blocks will be filled with information. We can ignore the _events_ block for now, as the _http_ block will have all our desired configurations. The _http_ block will hold all our servers that run with http, and of course, each server is hosted with it's own _server_ block, like the
following code:

```
	server {
		listen
		server_name

		location \ {
			root
			index
		}
	}
```

**Nginx Server Blocks**

These server blocks will hold all information regarding each respective server. In order to understand the server blocks, it is important to define each line.

listen - this will determine what port your server is held in server*name - this is where your server is held. Domain names often go here. If you would like to use your IP address, use an underscore (*)

root - this is the directory of what your server will hold index - this is for files in the directory that will be hosted. HTML and HTM files often go here

For now, let's try hosting our own server. Under the _http_ block, I will have a single server block. The server looks as so:

```
	server {
		listen 80;
		server_name _;

		location \ {
			root /file/location/directory
			index website.html
		}
	}
```

This server will be hosted on port 80 (http) and the browser address will be the user's IP address, as an underscore is used. For the files, the file is located in /file/location/directory and the file itself is named _website.html_.

With that done, open a browser and enter your IP address. You should see your HTML website.

**Your server is now hosted with nginx. Happy hosting!**
