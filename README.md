## Description: 
**monitor** is a web application that allows to view rrd datacollections that have been created by collectd (more info: http://collectd.org)

1- Monitor allow you to create group of server by projects.

2- Monitor allow to have different time zone for each server. Good, if you have distributed servers around the world.

3- Ready to talk with Mysql or SQLite, see the config file: modules/appsettings.py

4- Compatible with local authentication, LDAD and CASS, check the file: modules/appsettings.py

## Screenshots:

![Image](https://github.com/josedesoto/monitor/blob/master/static/images/monitor_app/monitor1.png?raw=true)
![Image](https://github.com/josedesoto/monitor/blob/master/static/images/monitor_app/monitor2.png?raw=true)
![Image](https://github.com/josedesoto/monitor/blob/master/static/images/monitor_app/monitor3.png?raw=true)


## How to install in Linux, windows or Mac:


1- Download web2py:

        #cd /opt
        #wget http://www.web2py.com/examples/static/web2py_src.zip

2- Desscompres:

        #unzip web2py_src.zip

3 - Download Stream log client into web2py:

        #cd /opt/web2py/applications
        #git clone https://github.com/josedesoto/monitor.git

4- Run web2py:

        #python /opt/web2py/web2py.py

5 - Open the URL: http://localhost:8000/monitor

6 - If you are using local login (settings.login_method='local') The application will show a registration page. This is the user you will use to access to the application.


## Dependecies:

Monitor is based in http://git.verplant.org/?p=collectd.git;a=blob;hb=master;f=contrib/collection.cgi for this reason need some extra packages.

In debian 6 or ubuntu 11:
	
	#apt-get install perl libjson-perl librrds-perl libhtml-entities-numbered-perl libhtml-element-extended-perl


## More configuration

For more configurations chenck the file: modules/appsettings.py

In this file you can configure the aplication to use Mysql or SQLite and the login system (local, ldap or CAS).


## How to update between versions:

Follow the installation before with the new version. Overwrite your configure file: appsettings.py and be sure you have the option settings.migrate = False. This mean, that the application will not try to create again the tables in the database. You have created with the version before.


## How to check the installations:

In your browser type:
	
	#http://localhost:8000/monitor/default/check_config


## Example to test it:

In the folder static/server_example you have some RRDD to start playing...


## How to install Collectd in Debian?

	#apt-get update
	#apt-get install librrd-dev rrdtool build-essential
	#wget http://collectd.org/files/collectd-5.0.4.tar.gz

	#tar xzf collectd-5.0.4.tar.gz
	#cd collectd-5.0.4
	#./configure
	#make all install

To add collectd daemon to start up initd:

	#insserv -v collectd

Information about the installation:

		Inhalation directory: /opt/collectd/
		Config file: /opt/collectd/etc/collectd.conf
		Data dir: /opt/collectd/var/lib/collectd


## Script collectd.sh
In private/script/bash you can find this script. You can use it for the start up init.d


## Script collectd_sync.sh
In private/script/bash you can find this script. You can use to sync the data from the clients to the web application. This script have to be in all server you install collectd daemon. To sync the data to the web application you have to use scheduled application. In cron for example:

	#*/30 * * * * PATH_TO_SCRIPT/collectd_sync.sh >> /dev/null


