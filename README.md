# Develop Inside a Docker Container
[VS Code](https://code.visualstudio.com/) has an extension, **Visual Studio Code Remote - Containers**, that allows us to use a docker container as a full-featured development environment. It allows us to open any folder inside (or mounted into) a container and take advantage of Visual Studio Code's full feature set. 

For PHP Development, this is the container we build in order to take advantage of this awesome feature!

## What's Inside?

We build the image off of the [BaseImage-PHP](https://github.com/BubbaOps/baseimage-php), which itself is built on [phusion/baseimage-docker](https://github.com/phusion/baseimage-docker) in order to give us a fully working OS for our development environment.

We provide builds for last few PHP releases, so it is trivial to change from one project to another when the projects use different versions of PHP. [BaseImage-PHP](https://github.com/BubbaOps/baseimage-php) gives us the following extensions out of the gate.


### Static Extension List
|            |            |           |          |
|------------|------------|-----------|----------|
| Core       | ctype      | date      | dom      |
| fileinfo   | filter     | ftp       | hash     |
| iconv      | json       | libxml    | pcre     |
| PDO        | Phar       | posix     | standard |
| Reflection | session    | SimpleXML | SPL      |
| tokenizer  | xml        | xmlreader | xmlwriter|

### Shared Extension List
|            |            |           |          |
|------------|------------|-----------|----------|
| bcmath     | bz2        | calendar  | curl     |
| exif       | gd         | gettext   | intl     |
| mbstring*  | mysqli     | mysqlnd   | opcache  |
| openssl*   | pcntl      | pdo_mysql | pdo_psql |
| pdo_sqlite | pdo_sqlsrv | pgsql     | readline*|
| redis      | soap       | sockets   | sodium   |
| sqlite3    | sqlsrv     | unixODBC  | xdebug   |
| xsl        | yaml       | zip*      | zlib*    |

_* These extensions are enabled by default._

### Pre-Installed Tools
There are some common tools that PHP Developers keep around, we have made it a point to pre-install them and ensure they are on the path.

* [@angular/cli](https://cli.angular.io/)
* [@vue/cli](https://cli.vuejs.org/)
* [bower](https://bower.io/)
* [Composer 2.0](https://getcomposer.org/)
* [git](https://git-scm.com/)
* [gulp](https://gulpjs.com/)
* [neovim](https://neovim.io/)
* [npm](https://www.npmjs.com/)
* [nvm](https://github.com/nvm-sh/nvm)
* [Pecl](https://pecl.php.net/)_*_
* [Pickle](https://github.com/FriendsOfPHP/pickle)
* [Python 3](https://www.python.org/)
* [yarn](https://classic.yarnpkg.com/en/)
* [zsh](https://www.zsh.org/)


_* Deprecated in PHP 7.4 try to use pickle instead._

## Versions
All images are currently based on Ubuntu 18.04 on which we provide standard php builds for PHP 7.2, 7.3, 7.4, and 8.0.



