<p align="center"><img src="https://cdn.jsdelivr.net/gh/cpriego/valet-linux-docs@master/assets/valet-logo.png"></p>

<p align="center">
<a href="https://packagist.org/packages/adesin-fr/valet-linux-ng"><img src="https://poser.pugx.org/cpriego/valet-linux/downloads.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/adesin-fr/valet-linux-ng"><img src="https://poser.pugx.org/cpriego/valet-linux/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/adesin-fr/valet-linux-ng"><img src="https://poser.pugx.org/cpriego/valet-linux/v/unstable.svg" alt="Latest Unstable Version"></a>
<a href="https://packagist.org/packages/adesin-fr/valet-linux-ng"><img src="https://poser.pugx.org/cpriego/valet-linux/license.svg" alt="License"></a>
</p>

## Introduction

Valet *Linux* **NG** is a Laravel development environment for Linux minimalists. No Vagrant, no `/etc/hosts` file. You can even share your sites publicly using local tunnels. _Yeah, we like it too._

Valet *Linux* **NG** configures your system to always run Nginx in the background when your machine starts. Then, using [DnsMasq](https://en.wikipedia.org/wiki/Dnsmasq), Valet proxies all requests on the `*.test` domain to point to sites installed on your local machine.

In other words, a blazing fast Laravel development environment that uses roughly 7MB of RAM. Valet *Linux* isn't a complete replacement for Vagrant or Homestead, but provides a great alternative if you want flexible basics, prefer extreme speed, or are working on a machine with a limited amount of RAM.

This fork is based on the work from **CPriego's Valet Linux** version of *Valet*, but it was lacking of `isolate` command which allows to run different versions of php depending of the folder ! 

## Official Documentation

Original Cpriego's Valet documentation can be found on the [Valet Linux website](https://cpriego.github.io/valet-linux/).

## Switching PHP version in a project

To switch from a version to another, just run `valet isolate [x.x]` in the project folder's, where `x.x` is the new version to use.
As an example, if your global php-fpm version is 8.0 and you want to run a projet to run with 7.4, just run `valet isolate 7.4`. Valet will try to install the corresponding version with your package manager.   

Valet NG relies on the php versions available in your package manager, it will not be able to install a version that is not known from your package manager !

Ubuntu users can use [Ondrej Sury's PPA](https://launchpad.net/~ondrej/+archive/ubuntu/php/) which provides php versions from 5.6 to 8.1. 

## How to use multiple CLI php versions ?

I found a trick which seems to do the job on 99% of my needs : 
* Edit your `.bashrc` (or {.zshrc}) to add the current directory to your `PATH`. ie. : `export PATH="./:$PATH"`. Be sure to include the current directory (`./`) **BEFORE** any other path.
* Close your terminal and open it again so your new `PATH` is applied.
* When a project needs a different PHP version, make a symlink in its directory to the needed php binary. ie : `ln -s /usr/bin/php7.4 php`.
* When you'll run i.e. `php artisan`, the current directory's php executable will be used.
* When you'll run `composer`, the `#!` starting line of composer, which is `/usr/bin/env`, will search php in your current PATH variable. So, because we set the current directory as the FIRST one to look, it will use the php symlink to run !  

## Testers wanted !

This version has only been tested on ubuntu 22.04. If you run a different distro and you are willing to try features that can break your system, please test it and report !

I'm running out of time to test it on other distros. If you have some free time, you can even fire a new virtual machine and test it under Arch, RedHat, and all other distro variants !

## License

Laravel Valet is an open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
