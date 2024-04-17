# SimpleGitAutoDeploy
This is a simple git auto deployment script. when you push your commits to your repository, this service automatically pulls commits and deploys your project on your server.

# How to use
#### Clone this project
Clone this project on your Linux server and open its dir
```
git clone https://github.com/amirhnir/SimpleGitAutoDeploy.git
```
```
cd SimpleGitAutoDeploy/
```
#### Config 
Look at the example.config.json and according to this, edit the config.json file as you need.
```
cat example.config.json
```
```
vi config.json
```
#### Create a Linux service
To run this script permanently, you need to create a Lunix service 
```
sudo vi /etc/systemd/system/simple-git-auto-deploy.service
```
This command creates a new service and you have to write some lines inside the file to specify what this service will do.
```
[Unit]
Description= Simple Git Auto Deploy 
After=syslog.target
After=network.target

[Service]
Type=simple
User=root
Group=root
ExecStart=/usr/bin/python /path/SimpleGitAutoDeploy.py

TimeoutSec=300

[Install]
WantedBy=multi-user.target
```
in the above code, you have to edit */path/SimpleGitAutoDeploy.py* to the real path of SimpleGitAutoDeploy.py file. also *User* and *Group* are set to *root* but it's better if you change these parameters to a normal user/group.

#### Start the service
```
sudo systemctl start simple-git-auto-deploy
sudo systemctl enable simple-git-auto-deploy
``` 