## Cloud Foundry PHP Buildpack

A buildpack for Cloud Foundry to deploy PHP based applications.


## 30 Second Tutorial

Getting started with the buildpack is easy.  With the `cf` command line utility installed, open a shell, change directories to the root of your PHP files and push your application using the argument `-b https://github.com/cloudfoundry/php-buildpack.git`.

Example:

```bash
mkdir my-php-app
cd my-php-app
cat << EOF > index.php
<?php
  phpinfo();
?>
EOF
cf push -m 128M -b https://github.com/cloudfoundry/php-buildpack.git my-php-app
```

Please note that you should change *my-php-app* to some unique name, otherwise you'll get an error and the push will fail.

The example above will create and push a test application, "my-php-app", to Cloud Foundry.  The `-b` argument instructs CF to use this buildpack.  The remainder of the options and arguments are not specific to the buildpack, for questions on those consult the output of `cf help push`.

Here's a breakdown of what happens when you run the example above.

  - On your PC...
    - It'll create a new directory and one PHP file, which calls `phpinfo()`
    - Run `cf` to push your application.  This will create a new application with a memory limit of 128M (more than enough here) and upload our test file.
  - On Cloud Foundry...
    - The buildpack is executed.
    - Application files are copied to the `htdocs` folder.
    - Apache HTTPD & PHP 5.4 are downloaded, configured with the buildpack defaults and run.
    - Your application is accessible at the URL http://<app-name>.cfapps.io (assuming your targeted towards Pivotal Web Services).

## More Information

While the *30 Second Tutorial* shows how quick and easy it is to get started using the buildpack, it skips over quite a bit of what you can do to adjust, configure and extend the buildpack.  The following docs and links provide a more in-depth look at the buildpack.

  - [Supported Software](#supported-software)
  - [Features](#features)
  - [Example Applications](#examples)
  - [Usage]
  - [Configuration Options]
  - [Composer]
  - [Binaries]
  - [Troubleshooting]
  - [Getting Help](#getting-help)
  - [Development]
  - [License](#license)
  - [Contributing](#contributing)

## Supported Software
* **Composer**
  * Composer 0.8
* **Web servers**
  * Apache 2.4
  * Nginx 1.5, 1.6, 1.7
* **PHP Versions**
  * PHP 5.4, 5.5, 5.6
  * HHVM 3.2
* **PHP Runtimes**
  * php-cli
  * php-cgi
  * php-fpm
  * hhvm
* **PHP Extensions**
  * amqp
  * apc
  * apcu
  * bz2
  * curl
  * dba
  * exif
  * fileinfo
  * ftp
  * gd
  * gettext
  * gmp
  * igbinary
  * imagick
  * imap
  * intl
  * ioncube
  * ldap
  * lua
  * mailparse
  * mbstring
  * mcrypt
  * memcache
  * memcached
  * mongo
  * msgpack
  * mysql
  * mysqli
  * opcache
  * openssl
  * pdo
  * pdo_mysql
  * pdo_pgsql
  * pdo_sqlite
  * pgsql
  * phalcon
  * phpiredis
  * pspell
  * redis
  * snmp
  * soap
  * sockets
  * suhosin
  * sundown
  * twig
  * xcache
  * xdebug
  * xhprof
  * xsl
  * yaf
  * zip
  * zlib
  * zookeeper
* **Third-Party Modules**
  * New Relic, in connected environments only.



## Features

Here's a list of some special features of the buildpack.

  - supports running commands or migration scripts prior to application startup
  - download location is configurable, allowing users to host binaries on the same network (i.e. run without an Internet connection)
  - supports an extension mechanism that allows the buildpack to provided additional functionality
  - allows for application developers to provide custom extensions
  - easy troubleshooting with the BP_DEBUG environment variable

## Examples

Here are some example applications that can be used with this buildpack.

  - [php-info]  This app has a basic index page and shows the output of phpinfo()
  - [PHPMyAdmin]  A deployment of PHPMyAdmin that uses bound MySQL services
  - [Wordpress]  A deployment of Wordpress that uses bound MySQL service
  - [CodeIgniter]  CodeIgniter tutorial application running on CF
  - [Stand Alone]  An example which runs a stand alone PHP script
  - [pgbouncer]  An example which runs the pgbouncer process in the container to pool db connections.
  - [phalcon]  An example which runs a Phalcon based application.
  - [composer] An example which uses Composer.

## Getting Help

If you have questions, comments or need further help with the buildpack you can post to the [vcap-dev] mailing list. It's a good place for posting question on all of the open source Cloud Foundry components, like this buildpack. Alternatively, if you're using Pivotal Web Services with the buildpack, you could post to the [support forums].

## License

The Cloud Foundry PHP Buildpack is released under version 2.0 of the [Apache License].

## Contributing

### Run the Tests

See the [Machete](https://github.com/cf-buildpacks/machete) CF buildpack test framework for more information.

### Package your own buildpack from this repo

`BUNDLE_GEMFILE=cf.Gemfile bundle exec buildpack-packager [ cached | uncached ]`


### Pull Requests

1. Fork the project
1. Submit a pull request

### Reporting Issues

This project is managed through Github.  If you encounter any issues, bug or problems with the buildpack please open an issue.

The project backlog is on [Pivotal Tracker](https://www.pivotaltracker.com/projects/1042066)

[Configuration Options]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md
[Development]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/development.md
[Troubleshooting]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/troubleshooting.md
[Usage]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/usage.md
[Binaries]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/binaries.md
[php-info]:https://github.com/dmikusa-pivotal/cf-ex-php-info
[PHPMyAdmin]:https://github.com/dmikusa-pivotal/cf-ex-phpmyadmin
[Wordpress]:https://github.com/dmikusa-pivotal/cf-ex-worpress
[CodeIgniter]:https://github.com/dmikusa-pivotal/cf-ex-code-igniter
[Stand Alone]:https://github.com/dmikusa-pivotal/cf-ex-stand-alone
[pgbouncer]:https://github.com/dmikusa-pivotal/cf-ex-pgbouncer
[Apache License]:http://www.apache.org/licenses/LICENSE-2.0
[vcap-dev]:https://groups.google.com/a/cloudfoundry.org/forum/#!forum/vcap-dev
[support forums]:http://support.run.pivotal.io/home
[Composer]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/composer.md
["offline" mode]:https://github.com/cloudfoundry/php-buildpack/blob/master/docs/binaries.md#bundling-binaries-with-the-build-pack
[phalcon]:https://github.com/dmikusa-pivotal/cf-ex-phalcon
[Phalcon]:http://phalconphp.com/en/
[composer]:https://github.com/dmikusa-pivotal/cf-ex-composer
