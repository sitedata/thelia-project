Readme
======

#### This is the project creation repository of Thelia. If you want to contribute, please take a look at [thelia/thelia](https://github.com/thelia/thelia)

Thelia
------
[![Build Status](https://travis-ci.org/thelia/thelia.png?branch=master)](https://travis-ci.org/thelia/thelia) [![License](https://poser.pugx.org/thelia/thelia/license.png)](https://packagist.org/packages/thelia/thelia) [![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/thelia/thelia/badges/quality-score.png?s=61e3e04a69bffd71c29b08e5392080317a546716)](https://scrutinizer-ci.com/g/thelia/thelia/)

[Thelia](http://thelia.net/) is an open source tool for creating e-business websites and managing online content. This software is published under LGPL.

This is the new major version of Thelia.

You can download this version and have a try or take a look at the source code (or anything you wish, respecting LGPL).  See http://thelia.net/ web site for more information.

A repository containing all thelia modules is available at this address : https://github.com/thelia-modules

Requirements
------------

* PHP 5.5
    * Required extensions :
        * PDO_Mysql
        * mcrypt
        * intl
        * gd
        * curl
    * safe_mode off
    * memory_limit at least 128M, preferably 256.
    * post_max_size 20M
    * upload_max_filesize 2M
    * date.timezone must be defined
* Web Server Apache 2 or Nginx
* MySQL 5

## Create a Thelia project

``` bash
$ curl -sS https://getcomposer.org/installer | php
$ php composer.phar create-project thelia/thelia-project path/ 2.4.0 (or 2.3.5)
```

## Install it with your own environment

You can install Thelia using the cli tool and the scripts provided by thelia/setup

``` bash
$ php Thelia thelia:install
```

Consult the page : http://localhost/thelia/web/index_dev.php

You can create a virtual host and choose web folder for root directory.

## Quick install with docker-compose

`Docker` and `docker-compose` have to be installed.

Build your docker containers on detached mode 
``` bash
$ docker-compose up -d
```

Enter in your container
``` bash
$ docker-compose exec php-fpm bash
```

Install thelia
``` bash
$ php Thelia thelia:install
```

By default if you haven't changed the `docker-compose.yml` you'll have to answer these questions like this

``` 
Database host [default: localhost] : mariadb
``` 
``` 
Database port [default: 3306] : 3306
```
``` 
Database name (if database does not exist, Thelia will try to create it) : thelia
```

``` 
Database username : thelia
```

``` 
Database pasword : thelia
```

Next just go to http://localhost:8080 and you should see your Thelia installed !

If you want add some sample data just execute this command (still in your container)
``` bash
$ php local/setup/import.php
```

If you want to access your database from your computer (with DBeaver, Sequel Pro or anything else) the host is `localhost` and the port is `8086` 

Documentation
-------------

Thelia documentation is available at http://doc.thelia.net

Roadmap
-------

The Roadmap is available at http://thelia.net/community/roadmap


Contribute
----------

See the documentation : http://doc.thelia.net/en/documentation/contribute.html

### Mac OSX

If you use Mac OSX, it still doesn't use php 5.4 as default php version... There are many solutions for you :

* use [phpbrew](https://github.com/c9s/phpbrew)
* use last MAMP version and put the php bin directory in your path:

```bash
export PATH=/Applications/MAMP/bin/php/php5.5.x/bin/:$PATH
```

* configure a complete development environment : http://php-osx.liip.ch/
* use a virtual machine with vagrant and puppet : https://puphpet.com/

### MySQL 5.6

As of MySQL 5.6, default configuration sets the sql_mode value to

```
STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION
```

This 'STRICT_TRANS_TABLES' configuration results in SQL errors when no default value is defined on NOT NULL columns and the value is empty or invalid.

You can edit this default config in ` /etc/my.cnf ` and change the sql_mode to remove the STRICT_TRANS_TABLES part

```
[mysqld]
sql_mode=NO_ENGINE_SUBSTITUTION
```

Assuming your sql_mode is the default one, you can change the value directly on the run by running the following SQL Command

```sql
SET @@GLOBAL.sql_mode='NO_ENGINE_SUBSTITUTION', @@SESSION.sql_mode='NO_ENGINE_SUBSTITUTION'
```

For more information on sql_mode you can consult the [MySQL doc](http://dev.mysql.com/doc/refman/5.0/fr/server-sql-mode.html "sql Mode")

## Archive builders
Thelia's archive builder's needs external libraries.
For zip archives, you need PECL zip. See [PHP Doc](http://php.net/manual/en/zip.installation.php)

For tar archives, you need PECL phar. Moreover, you need to deactivate php.ini option "phar.readonly":
```ini
phar.readonly = Off
```

For tar.bz2 archives, you need tar's dependencies and the extension "bzip2". See [PHP Doc](http://php.net/manual/fr/book.bzip2.php)

For tar.gz archives, you need tar's dependencies and the extension "zlib". See [PHP Doc](http://fr2.php.net/manual/fr/book.zlib.php)
