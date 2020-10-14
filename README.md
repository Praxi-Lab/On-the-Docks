# docker-app

## Description
A mobile app that helps you run commands on your terminal remotely.
Currently the app supports **Quick Docker** Commands to make your workflow even easier.

## Getting Started

This guide shall explain how to setup this application on your system for development purposes.

**Pre-requisites:**

* Linux system (CentOS7, RHEL 8 etc)
* Docker 19.03 or above
* Python 3.6+

### Cloning the Repository
Fork the repository and then clone the forked repository to your system.

```shell
$ git clone https://github.com/<your-username>/docker-app.git
$ cd docker-app
$ git remote add upstream https://github.com/hemabhravee/docker-app.git
$ git fetch --all
```

### Setting up a development environment
**Step 1**: The application requires to setup an Apache Server to make HTTP requests from and to the system.

```shell
$ yum install httpd
```
**Step 2**: Copy the script to the `cgi-bin` folder and make it an executable.

```shell
$ chmod +x script.py
$ cp script.py /var/www/cgi-bin/
```

**Step 3**: Disabling SE Linux is an important step for development practices, for a production build this shall not be necessary.
To disable SE Linux and set server permissions

```shell
$ setenforce 0
$ sudo usermod -a -G docker apache
```
This adds `apache` to the group `docker`. 
Without doing this, we can't use "remove all docker containers" command

**Step 4**: Add the following line to `/etc/sudoers`

```txt
apache ALL=(ALL)    NOPASSWD: ALL
```

Before running the app, change url. 
