# SurgeWP Vagrant
A Vagrant configuration that incorporates the [SurgeWP Skeleton](https://github.com/SurgeWP/surgewp-skeleton). Currently being battle tested at [SurgeWP](http://www.surgewp.com/).

  * **Version**: 0.1.0
  * **Contributors**:
    * Connor Black 
      * Github: [@connorblack](http://github.com/connorblack)
      * Twitter: [@connorjblack](https://twitter.com/connorjblack)
    * **Contributing**: We love contributors! Please submit pull requests against the master branch.

### What You Get

  * A robust Vagrant development environment based off of [Varying Vagrant Vagrants](https://github.com/10up/varying-vagrant-vagrants)
  * Out of the box incorporation with the [SurgeWP Skeleton](https://github.com/SurgeWP/surgewp-skeleton), which includes:
    * WordPress 3.6.1
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
2. Install [Vagrant 1.3.5](http://downloads.vagrantup.com/tags/v1.3.5)
3. Install the [vagrant-hostsupdater](https://github.com/cogitatio/vagrant-hostsupdater)

  ```
  $ vagrant plugin install vagrant-hostsupdater
  ```
4. Clone SurgeWP Vagrant (make sure to either delete the `.git` in the root or to never push from root, unless you're explicitly commiting to the SurgeWP Vagrant core):

  ```
  $ git clone git://github.com/SurgeWP/surgewp-vagrant.git <project name>
  ```
5. Change directories into your project folder, start Vagrant, and let the machine provision (it should take a few minutes):

  ```
  $ cd <project name>
  $ vagrant up
  ```
6. Change directories to the `www/surgewp-skeleton/` root and change the git remote to point towards your github repository (if it doesn't exist, log into your github account and create it - the `www/surge-skeleton/` root is where you should be doing most of your coding, commits, and deployments):

  ```
  $ git remote set-url origin git://your.git.repository
  ```
7. Make sure the database credientials in `www/surgewp-skeleton/local-config.php` match the SurgeWP Vagrant database.
8. Go to [http://local.surgewp-skeleton.dev/wp/wp-admin/install.php](http://local.surgewp-skeleton.dev/wp/wp-admin/install.php) and install WordPress.
9. After the install, log in and go to the `Settings -> General` section.
  * Find where it says `Site Address (URL)`.
  * Change it from `local.surgewp-skeleton.dev/wp` to `local.surgewp-skeleton.dev`
  * Don't change the section `WordPress Address (URL)`!

### Deployment with Capistrano
#### `config.rb`

1. Open `config/config.rb`.
2. Set your application title:

  ```
  set :application, "Appication title"
  ```
3. Set your github repository (make sure it's read only, or else you'll have to add a deploy SSH key to github):

  ```
  set :repository,  "Set your git repository location here"
  ```
4. Set where on the server the production files will be deployed to:
  
  ```
  set :production_deploy_to, '/www/example.com'
  ```
5. Set the domain name for staging:

  ```
  set :staging_domain, 'staging.example.com'
  ```
6. Set the user that Capistrano will use to SSH into the server with and set the sudo flag. Make sure it has all the necessary permissions (you'll almost always use your username which should have the proper permissions):

  ```
  set :user, "username"
  set :use_sudo, true
  ```
7. Give the proper database credentials:

  ```
  set :wpdb do
  	{
  		:production => {
  			:host     => 'PRODUCTION DB HOST',
  			:user     => 'PRODUCTION DB USER',
  			:password => 'PRODUCTION DB PASS',
  			:name     => 'PRODUCTION DB NAME',
  		},
  		:staging => {
  			:host     => 'STAGING DB HOST',
  			:user     => 'STAGING DB USER',
  			:password => 'STAGING DB PASS',
  			:name     => 'STAGING DB NAME',
  		}
  	}
  end
  ```
  
#### `staging.rb`
1. Open `config/staging.rb`.
2. Set on the server where the staging files will be deployed to:

  ```
  set :deploy_to, "/www/example.com"
  ```
3. Set the staging server domain address:

  ```
  role :web, "00.000.0.00"
  ```
  
#### `production.rb`
1. Open `config/production.rb`.
2. Set on the server where the production files will be deployed to:

  ```
  set :deploy_to, "/www/example.com"
  ```
3. Set the production server domain address:

  ```
  role :web, "00.000.0.00"
  ```

### Finalizing
1. Edit the `.gitignore` to look like this:

  ```
  /shared
  /sql-dump-*.sql
  /db-sync
  /content/upgrade/
  /node_modules/
  ```
2. Install NPM dependencies:

  ```
  npm install
  ```
3. Start Grunt and make changes to the starter theme:
  
  ```
  grunt watch
  ```
4. Push your code:
  
  ```
  $ git add .
  $ git commit -m "commit message"
  $ git push -u origin --all
  ```
5. Run Capistrano setup and deploy to staging:
  
  ```
  $ cap deploy:setup
  $ cap staging deploy
  ```
6. Other Capistrano commands:
  
  ```
  $ cap production deploy # Deploys to production
  $ cap deploy:rollback   # Rolls back the last deploy
  ```
  
