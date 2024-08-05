# Install Laravel on Mac m1
Setting up Laravel on a Mac M1 can significantly enhance your development workflow, given the powerful performance of Apple’s latest silicon. Laravel, known for its elegant syntax and robust capabilities, requires a few additional steps to ensure compatibility with the M1 architecture. In this guide, we’ll walk you through the streamlined process of installing Laravel on your Mac M1, from configuring your environment to overcoming any specific challenges. Whether you're new to Laravel or a seasoned developer, this guide will help you get up and running efficiently. please following this step.

### - Installing Brew
Brew (https://brew.sh/) is a crucial package manager for macOS that's currently absent from your system. To get it set up, open your terminal and execute:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Verify the installation of brew by running the following command:

```
user@macbook-user ~ % brew --version
Homebrew 4.3.13
```

### - Installing multiple Version PHP
next, we’ll walk through the steps to install multiple PHP versions simultaneously, allowing you to easily switch between different versions based on your project's requirements. following this command

```
brew tap shivammathur/php
```
Next, you can install all the PHP versions you require, including versions from 5.6 up to 8.0 

```
brew install shivammathur/php/php@5.6
brew install shivammathur/php/php@7.0
brew install shivammathur/php/php@7.1
brew install shivammathur/php/php@7.2
brew install shivammathur/php/php@7.3
brew install shivammathur/php/php@7.4
brew install shivammathur/php/php@8.0
```
For more details, visit the source at [link](https://medium.com/macoclock/how-to-install-multiple-php-versions-on-macos-1f290c32cd63#:~:text=Install%20multiple%20versions%20of%20PHP).

After the installation is complete, add the following code to your .zshrc file.
```
switchphp() {
    installed_php_versions=("7.4" "8.0" "8.1" "8.2" "8.3")
    current_php_version=$(php -v | grep -o 'PHP [0-9]*\.[0-9]*' | cut -d ' ' -f 2 | sed -e 's/^[[:space:]]*//' -e 's/[[:space:]]*$//')
    target_php_version=$1
    
    if [ -z "$1" ]; then
        echo "No PHP version provided"
        return 1
    fi
    
    if [[ ! ${installed_php_versions[(r)$target_php_version]} ]]; then
        echo "Invalid PHP version provided"
        return 1
    fi
    
    if [[ $target_php_version == $current_php_version ]]; then
        echo "You are already on PHP version $1"
        return 1
    fi
    
    brew unlink php@"$current_php_version"
    brew link php@"$target_php_version"
    php -v
}
```
If you encounter any issues, refer to the information below, as the problems may be due to the recent installation.
```
switchphp:2: command not found: php
Error: No such keg: /opt/homebrew/Cellar/php@
```
like
```
user@macbook-user ~ % switchphp 7.4
switchphp:2: command not found: php
Error: No such keg: /opt/homebrew/Cellar/php@
Linking /opt/homebrew/Cellar/php@7.4/7.4.33_6... 25 symlinks created.

If you need to have this software first in your PATH instead consider running:
  echo 'export PATH="/opt/homebrew/opt/php@7.4/bin:$PATH"' >> ~/.zshrc
  echo 'export PATH="/opt/homebrew/opt/php@7.4/sbin:$PATH"' >> ~/.zshrc
PHP 7.4.33 (cli) (built: Aug  1 2024 07:06:15) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.33, Copyright (c), by Zend Technologie
```
To check your PHP version, run the command `php -v`, and if needed, install a different version. After installing a new version, try running the command `switchphp 7.4` to switch to PHP 7.4 or if you want use version 8.1 you can try running the command `switchphp 8.1`.

For more details, visit the source at [link](https://fsylum.net/blog/simple-php-switching-zsh-function/#:~:text=Quick%20note%3A%20We%20can%20use%20shivammathur/homebrew%2Dphp%20to%20install%20any%20PHP%20older%20than%208.0.).

### - Installing Composer
To install Composer for Laravel using Homebrew on macOS, you can use the following command:

```
brew install composer
```
If you encounter an error after installing composer like the one below, run the command `switchphp 7.4`, then run `brew install composer`
again..
```
Already downloaded: /Users/ivannofickadhanugraha/Library/Caches/Homebrew/downloads/bf9f18c1224a72004ddf6d70ba0203e570251c8223efea7284955158db329dd0--php-8.3.10.bottle_manifest.json
==> Pouring php--8.3.10.arm64_sonoma.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /opt/homebrew
Could not symlink bin/pear
Target /opt/homebrew/bin/pear
is a symlink belonging to php@7.4. You can unlink it:
  brew unlink php@7.4

To force the link and overwrite all conflicting files:
  brew link --overwrite php

To list all files that would be deleted:
  brew link --overwrite php --dry-run

Possible conflicting files are:
/opt/homebrew/bin/pear -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/pear
/opt/homebrew/bin/peardev -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/peardev
/opt/homebrew/bin/pecl -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/pecl
/opt/homebrew/bin/phar -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/phar
/opt/homebrew/bin/phar.phar -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/phar.phar
/opt/homebrew/bin/php -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/php
/opt/homebrew/bin/php-cgi -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/php-cgi
/opt/homebrew/bin/php-config -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/php-config
/opt/homebrew/bin/phpdbg -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/phpdbg
/opt/homebrew/bin/phpize -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/phpize
/opt/homebrew/sbin/php-fpm -> /opt/homebrew/Cellar/php@7.4/7.4.33_6/sbin/php-fpm
Error: Could not symlink include/php/TSRM/TSRM.h
Target /opt/homebrew/include/php/TSRM/TSRM.h
is a symlink belonging to php@7.4. You can unlink it:
  brew unlink php@7.4

To force the link and overwrite all conflicting files:
  brew link --overwrite php@7.4

To list all files that would be deleted:
  brew link --overwrite php@7.4 --dry-run
```
After the installation is successful, check the Composer version by running the command `composer --version`. then the command return like below
```
user@macbook-user ~ % composer --version
Composer version 2.7.7 2024-06-10 22:11:12
PHP version 7.4.33 (/opt/homebrew/Cellar/php@7.4/7.4.33_6/bin/php)
Run the "diagnose" command to get more detailed diagnostics output.
```
after successfully install composer, put and save the command bellow line on `.zshrc` and then reopen terminal
```
export PATH=$PATH:$HOME/.composer/vendor/bin
```

for more details, visit the source [link](https://gist.github.com/bradtraversy/b58f74cd863a465068eaeaae1544d9be#install-composer-php-dependency-manager:~:text=Install%20composer%20(PHP%20Dependency%20Manager))

### - Install Valet with Composer
Valet is a local development tool that simplifies setting up a local server environment for PHP applications.

To execute the command, open your terminal or command prompt and type:
```
composer global require laravel/valet
```
next run command for check version valet
```
valet --version
```
terminal return like below

```
user@macbook-user ~ % valet --version
Laravel Valet 4.7.1
```

for more details install valet you can visit the source [link](https://gist.github.com/bradtraversy/b58f74cd863a465068eaeaae1544d9be#install-valet-with-composer)
