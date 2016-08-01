..  -*- mode: rst -*-
..  -*- coding: utf-8 -*-

# Using this class

I'm using this class for development use in laravel 5 on windows machine.
This class simulates the real memcached php extension in windows which actually doesn't exist yet (php_memcached.dll).

## Configuration

Before you do anything else, make sure you have **memcached server** installed. Here's a blog that shows how to do that (follow setp A): https://commaster.net/content/installing-memcached-windows

Assuming you have memcached server isntalled, proceed with the following.

Place **memcached.php** file in **C:\xampp\php\pear** folder

In your laravel 5 installation, edit **AppServiceProvider.php** and place the code below inside the boot() method.


::

    if (!class_exists('Memcached')) {
        include ("memcached.php");
    }


so it should looks something like:


::

    public function boot(Kernel $kernel)
    {
        if (!class_exists('Memcached')) {
            include ("memcached.php");
        }
    }


===========================================================================
PHP Memcached Client (simulator)
===========================================================================



As there has no php memcached extension for windows now, it's difficult to
build develop envionment, so this class will be helpful.

Inspried by: http://github.com/joonas-fi/xslib-memcached


Usage:

Just as php_memcached extension, new Memcached object and etc.

::

    $m = new Memcached();
    $m->addServer('localhost', 11211);

    $m->set('foo', 'bar');
    $m->get('foo');


Supported method:

-   addServer
-   addServers
-   delete
-   get
-   getOption
-   getResultCode
-   getResultMessage
-   getServerList
-   increment
-   set
-   setOption
-   setOptions
-   getVersion
-   flush

Need disable memcached extension of PHP to run PHPUnit testcase.


License: MIT
