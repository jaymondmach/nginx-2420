Setting up a Simple Web Server with Nginx on Ubuntu
In this tutorial, we'll walk through setting up a basic web server using Nginx on Ubuntu. Nginx is a popular open-source web server known for its high performance, stability, and low resource consumption.

Prerequisites
A machine running Ubuntu.
sudo access or root privileges.
Step 1: Install Nginx
First, we need to install Nginx. Open a terminal and run the following commands:

bash
Copy code
sudo apt update
sudo apt install nginx
This will update the package index and install Nginx on your system.

Step 2: Start Nginx
Once installed, Nginx should start automatically. To verify that it's running, you can use the following command:

bash
Copy code
sudo systemctl status nginx
If Nginx is running, you should see an output indicating that it's active and running.

Step 3: Configure Firewall
If you have a firewall enabled, you need to allow traffic on port 80 (HTTP) so that users can access your web server. Run the following command to enable HTTP traffic:

bash
Copy code
sudo ufw allow 'Nginx HTTP'
Step 4: Test Nginx
Now that Nginx is installed and running, let's test it. Open a web browser and enter your server's IP address in the address bar. You should see the default Nginx landing page.

Step 5: Serve a Custom Page
To serve a custom HTML page, create a new file in the /var/www/html directory. You can name the file whatever you like, but for this example, let's create a file named index.html:

bash
Copy code
sudo vim /var/www/html/index.html
Paste the following HTML code into the file:

html
Copy code

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Custom Page</title>
</head>
<body>
    <h1>Hello, world!</h1>
    <p>This is a custom page served by Nginx.</p>
</body>
</html>
Save and close the file.

Step 6: Restart Nginx
After creating the custom HTML file, you need to restart Nginx for the changes to take effect:

bash
Copy code
sudo systemctl restart nginx
Step 7: Test Custom Page
Finally, open a web browser and enter your server's IP address again. You should now see your custom HTML page displayed.

That's it! You've successfully set up a simple web server using Nginx on Ubuntu.

Conclusion
In this tutorial, we covered the basics of setting up a web server with Nginx on Ubuntu. You learned how to install Nginx, serve a custom HTML page, and test your server. Feel free to explore more advanced configurations and features offered by Nginx to further customize your web server.
