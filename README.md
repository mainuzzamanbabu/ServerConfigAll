## PM2 process(For react, Nodejs based)


Install PM2 globally:
npm install pm2 -g


pm2 start npm -- start


pm2 start [script_file_name].js


pm2 list

pm2 stop [process_id]
 
pm2 restart [app-name/id]



pm2 delete my-project
pm2 start npm --name "my-project" -- start
HTTPS=true pm2 start npm --name "my-project" -- start

The configuration File: 




## Using systemd to run Django project

To keep your Django project running even after you close the Putty connection, you can use a process manager like systemd. Here are the steps you can follow:

Create a systemd service file for your Django project. You can create a new file at /etc/systemd/system/your_project.service and add the following contents:
------------
[Unit]
Description=Your Django project
After=network.target

[Service]
User=your_username
Group=www-data
WorkingDirectory=/path/to/your/project/
ExecStart=/path/to/your/virtualenv/bin/gunicorn your_project.wsgi:application --bind 127.0.0.1:8000

[Install]
WantedBy=multi-user.target
-------------

Modify the User, Group, WorkingDirectory, ExecStart fields in the above file to match your own configuration.

Save and close the file.

Reload the systemd daemon to pick up the changes:

-> sudo systemctl daemon-reload

Start the service:

-> sudo systemctl start your_project

Enable the service to start automatically on boot:

-> sudo systemctl enable your_project

Check the status of the service to ensure it is running:

-> sudo systemctl status your_project

You should now be able to access your Django project at http://127.0.0.1:8000 even after you close the  connection.





