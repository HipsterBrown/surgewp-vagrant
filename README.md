# SurgeWP Vagrant
A Vagrant configuration that incorporates the [SurgeWP Skeleton](https://github.com/SurgeWP/surgewp-skeleton). Currently being battle tested at [SurgeWP](http://www.surgewp.com/).

  * **Version**: 0.0.1
  * **Contributors**:
    * Connor Black 
      * Github: [@connorblack](http://github.com/connorblack)
      * Twitter: [@connorjblack](https://twitter.com/connorjblack)
    * **Contributing**: We love contributors! Please submit pull requests against the master branch.

### What You Get

  * A robust Vagrant development environment based off of [Varying Vagrant Vagrants](https://github.com/10up/varying-vagrant-vagrants)
    * After the install, visit any of the following default sites in your browser:
      * http://local.surgewp-skeleton.dev/ for your WordPress dev site
      * http://surgewp.dev/ for a default dashboard containing several useful tools
  * Out of the box incorporation with the [SurgeWP Skeleton](https://github.com/SurgeWP/surgewp-skeleton), which includes:
    * WordPress 3.8
    * [Roots](http://roots.io/) starter theme (with [Bootstrap](http://getbootstrap.com/) goodness)
    * [Grunt](http://gruntjs.com/) workflow
    * [Capistrano](http://www.capistranorb.com/) and deployment recipes 

### Overview

  * `config/`: main configurations for the server technologies
  * `database/`: databases, scripts and backups
  * `provision/`: server provisioning script
  * `www/`: web root
  * `Vagrantfile`: Vagrant configuration file

### Getting started

1. Install [VirtualBox 4.3.2](https://www.virtualbox.org/wiki/Downloads)
2. Install the latest version of [Vagrant](http://www.vagrantup.com/downloads.html)
3. Install the [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater)

  ```
  $ vagrant plugin install vagrant-hostsupdater
  ```
4. Clone SurgeWP Vagrant:

  ```
  $ git clone git://github.com/SurgeWP/surgewp-vagrant.git <workspace name>
  ```
5. Change directories into your workspace folder, start Vagrant, and let the machine provision (it should take a few minutes):

  ```
  $ cd <workspace name>
  $ vagrant up
  ```
6. Change directories to the `www/` folder and create a new project using the SurgeWP Skeleton (guide can be found at the SurgeWP Skeleton [repo](https://github.com/SurgeWP/surgewp-skeleton#surgewp-skeleton)).

7. Once you have configured everything you should be able to restart SurgeWP Vagrant and start working on your new site:

  ```
  $ vagrant reload --provision
  ```
  
