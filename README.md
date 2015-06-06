Todo-Laravel
============

## Clone Vagrantfile

https://github.com/scotch-io/scotch-box

    git clone https://github.com/scotch-io/scotch-box.git todo
    cd todo

## Launch Server

    vagrant up

http://192.168.33.10/

## Create Project

    vagrant ssh
    vagrant@scotchbox:/$ cd /var/www
    vagrant@scotchbox:/var/www$ laravel new laravel
    vagrant@scotchbox:/var/www$ rm -rf public/
    vagrant@scotchbox:/var/www$ mv laravel/public .

## public/index.php

Change line 21 from `require __DIR__.'/../bootstrap/autoload.php';` to `require __DIR__.'/../laravel/bootstrap/autoload.php';` and line 35 from `require __DIR__.'/../bootstrap/app.php';` to `require __DIR__.'/../laravel/bootstrap/app.php';`.

    <?php
    /**
     * Laravel - A PHP Framework For Web Artisans
     *
     * @package  Laravel
     * @author   Taylor Otwell <taylorotwell@gmail.com>
     */

    /*
    |--------------------------------------------------------------------------
    | Register The Auto Loader
    |--------------------------------------------------------------------------
    |
    | Composer provides a convenient, automatically generated class loader for
    | our application. We just need to utilize it! We'll simply require it
    | into the script here so that we don't have to worry about manual
    | loading any of our classes later on. It feels nice to relax.
    |
    */

    require __DIR__.'/../todo/bootstrap/autoload.php';

    /*
    |--------------------------------------------------------------------------
    | Turn On The Lights
    |--------------------------------------------------------------------------
    |
    | We need to illuminate PHP development, so let us turn on the lights.
    | This bootstraps the framework and gets it ready for use, then it
    | will load up this application so that we can run it and send
    | the responses back to the browser and delight our users.
    |
    */

    $app = require_once __DIR__.'/../todo/bootstrap/app.php';

    /*
    |--------------------------------------------------------------------------
    | Run The Application
    |--------------------------------------------------------------------------
    |
    | Once we have the application, we can handle the incoming request
    | through the kernel, and send the associated response back to
    | the client's browser allowing them to enjoy the creative
    | and wonderful application we have prepared for them.
    |
    */

    $kernel = $app->make('Illuminate\Contracts\Http\Kernel');

    $response = $kernel->handle(
      $request = Illuminate\Http\Request::capture()
    );

    $response->send();

    $kernel->terminate($request, $response);
