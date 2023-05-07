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

#nginx config file for Nextjs App
#place in /etc/nginx/sites-available/name_of_config_file
server {
        listen 80;
        server_name server_url/IP;

        gzip on;
        gzip_proxied any;
        gzip_types application/javascript application/x-javascript text/css text/plain text/xml application/xml application/xml+rss;

        gzip_comp_level 5;
        gzip_buffers 16 8k;
        gzip_min_length 256;

        location /_next/static/ {
                alias /path/.next/static/;
                expires 365d;
                access_log off;
        }

        location / {
                proxy_pass http://127.0.0.1:3000; #change to 3001 for second app, but make sure second nextjs app starts on new port in packages.json "start": "next start -p 3001",
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }
        location /writebot/_next/static/ {
                alias /home/aiasstproject/AiAsstFinalFront/.next/static/;
                expires 365d;
                access_log off;
        }
        location /writebot/ {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        rewrite ^/writebot(.*)$ $1 break;
    }
        location /serverapi/ {
                proxy_pass http://127.0.0.1:8080/;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
    }
        location /aiapi/ {
                proxy_pass http://127.0.0.1:8000/;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }


}



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





