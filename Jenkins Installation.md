## Installation
```sh
wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```
## Port configuration
edit ```sudo nano /etc/default/jenkins```
and Change the port with
```HTTP_PORT=8081```

## Start Jenkins
sudo service jenkins start

## Stop Jenkins
sudo service jenkins stop
