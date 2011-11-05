Tattle  (formely Graphite-Tattle)
======

A self service alerting and dashboard frontend for [graphite][graphite]

This tool was first presented at [EscConf][escconf] during a presentation by drowe from [Wayfair][wayfair]

Concepts
--------

* *Checks*
  A Check is a [graphite][graphite] target in combination with a user defined Error and Warning threshold. 

* *Subscriptions*
  A Subscription is a users signing up for to be alerted by a plugin if the Check reaches the Error or Warning state. A user can have multiple subscriptions to an alert based on different threshold and plugins. (Example : SMS for Error, and Email for Warning)

* *Alerts*
  An Alert is the signal that the Check either passed it's defined Error or Warning threshold, or it's returned to the OK state from being in a bad state. The frequency of Alerts is defined by the Repeat Delay (in minutes), which can't be less than the frequency of the processing cronjob. 

* *Dashboards*
  A Dashboard is a collection of pre-defined graphs that allows for self service creation and has a fullscreen option.

* *Graph*
  A Graph in Tattle is a combination of "lines" which make up the graph. A graph can have one or more lines, and can set the display type of the graphs (Stacked or Not) and has a weight for ordering on the dashboard.

* *Lines*
  Lines are a combination of an Alias, a graphite Target, and a color.


Installation Requirements
-----------------------------

* PHP
* MySQL
* Lighttpd / NGINX / Apache
* [Flourishlib][flourishlib] for the PHP framework  
* [bootstrap][bootstrap] for the HTML/CSS framework
* http access to a [graphite][graphite] installation


Installation and Configuration
-----------------------------
* Import .sql file to create database and tables

* Create a session storage folder for flourishlib

* Create JS/CSS minification directory and allow Apache to write to it. By default this is 
   /js_cache e.g.

  install -o www-data /var/www/js_cache/images

* Create a file called inc/config.override.php so that upgrades don't blow away your config
  
  Your config.override might look something like this:
--------------------------
  <?
   $GLOBALS['DATABASE_NAME'] = 'graphite_tattle';
   $GLOBALS['DATABASE_USER'] = 'tattle';
   $GLOBALS['DATABASE_PASS'] = 'yoyoyo';
   $GLOBALS['GRAPHITE_URL'] = 'http://graph';
--------------------------
  
* Edit inc/config.php with the correct settings (Examples db password)

* Setup cronjob to to run processor.php. This file can be run either as a cli or through the web server. (cli maybe required depending on your plugins and their required permissions)

* Register via the web interface. (The first user registered is the admin currently prior to us implementing any roles, and other permissions)


Reason for creation
-----------

[StatsD][statsd] from the team over at [Etsy][etsy] added a simple Dev and Ops friendly way to send metrics to graphite.
[graphite][graphite] makes graphing metrics and data self serve and simple for anyone. 

With this tag team in our environment alerting seemed to be the weakest link from an adhoc/self service perspective which is where the idea
for Tattle came from.

Caution!
----------
This project is still in an Alpha status and not feature complete or ready for full production use yet.
Any help smoothing out the edges and adding additional features / functions would be greatly appreciated!

How to Contribute
---------------------

You're interested in contributing to Tattle? Sweet!

fork Tattle from here: http://github.com/wayfair/Graphite-Tattle

1. Clone your fork
2. Hackit up
3. Push the branch up to GitHub
4. Send a pull request to the wayfair/Graphite-Tattle project.

We'll do our best to get your changes in as soon as possible!

[graphite]: http://graphite.wikidot.com
[etsy]: http://www.etsy.com
[statsd]: https://github.com/etsy/statsd/
[bootstrap]: http://twitter.github.com/bootstrap/
[flourishlib]: http://flourishlib.com
[escconf]: http://escconf.com
[wayfair]: http://engineering.wayfair.com/


