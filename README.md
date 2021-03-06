# README

## Introduction

MopaBarcodeBundle integrates Zend_Barcode and PHP QR Lib to be easily used in symfony2 via twig.
I did include phpqrcode form  http://sourceforge.net/projects/phpqrcode/ due to changes in its config.
Is just a shot and shouldnt be considered to be perfect. Feel free to fork and PR.

## Prerequisites

## Installation

1.1 Add this bundle to your project as via deps:


```
[MopaBarcodeBundle]
    git=http://github.com/phiamo/MopaBarcodeBundle.git
    target=/bundles/Mopa/BarcodeBundle
```

1.2 Or add this bundle to your project as a Git submodule:

``` bash
git submodule add git@github.com:phiamo/MopaBarcodeBundle.git vendor/bundles/Mopa/BarcodeBundle
```

2. Add namespace to you app/autoload.php

``` php
<?php
// app/autoload.php
$loader->registerNamespaces(array(
    // ...
    'Mopa'        => __DIR__.'/../vendor/bundles',
));
```

3. Add this bundle to your app/AppKernel.php:

``` php
// application/ApplicationKernel.php
public function registerBundles()
{
    return array(
        // ...
        new Mopa\BarcodeBundle\MopaBarcodeBundle(),
        // ...
    );
}
```

## Optionally install Zend Framework 2 (maybe you can only use the Barcode and Validator Subtrees, never tried)
I did include phpqrcode form  http://sourceforge.net/projects/phpqrcode/ due to changes in its config

either via deps:

```
[Zend]
    git=http://github.com/zendframework/zf2.git

```

or as git submodule

``` bash
git submodule add git://github.com/zendframework/zf2.git vendor/Zend
```


## Demo

Include MopaBoostrapBundle in your app: https://github.com/phiamo/MopaBootstrapBundle

Include this snipplet in your routing.yml

``` yaml
my_barcode_playground:
    resource: "@MopaBarcodeBundle/Resources/config/routing/barcode_playground.yml"
    prefix:   /
```

And try http://{yoursymfonyapp}/barcode/playground

## Usage

Have a look into the https://github.com/phiamo/MopaBarcodeBundle/blob/master/Controller/BarcodeController.php
to see it in action

Supported Barcode Types depend on your Zend2 installation

If you installed it have a look into
https://github.com/phiamo/MopaBarcodeBundle/blob/master/Model/BarcodeTypes.php
The Type given to the service is either the int or the string defined in the types arrays keys and values

To get the service use in your controllers etc you can use 

$bmanager = $this->container->get('mopa_barcode.barcode_service');

$bmanager->saveAs($type, $text, $file);
to save a Barcode of $type with $text as $file or

$bmanager->get($type, $enctext, $absolute = false);
to get the url to the file
where $enctext is urlencoded and $absolute is an boolean to get either the absolute or the relative path (default)

## Twig Helper 

There is also a twig helper registered:

``` jinja
        <p><img alt="[barcode]" src="{{ mopa_barcode_url('code128', '123456789') }}"></p>
```

## Using the bundle directly

To Make usage e.g. of the Playground in your app, just copy the playground.html.twig to
app/Resources/MopaBootstrapBundle/views/Barcode/playground.html.twig 
and modify as you like

## Using the Bundle as a urlservice

If you would like to generate the barcodes on the fly include
in your routing.yml

``` yaml
my_barcode_display:
    resource: "@MopaBarcodeBundle/Resources/config/routing/barcode_display.yml"
    prefix:   /
```
And just use Urls to generate your barcodes:

http://{yoursymfonyapp}/barcode/send/{type}/{enctext}

## TODO

    - Load the different Barcode Libs in a different way. should't be done by ints :(
 
 
## Known Issues

    - Nothing what could not be done in another way, probably some will arise as soon as its published
      So make issues!
    - There are probably things missing, so make PR's 
