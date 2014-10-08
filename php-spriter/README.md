# Readme - PHP Spriter

PHP Spriter ...

* is an easy to use and flexible icon sprite generator
* generates png sprite(s) and associated css file on the fly

Creator: [Christian Stuff](https://github.com/regaddi) 
Hosted on: [GitHub](http://namics.github.io/php-spriter/)

## Installation

You need:

* PHP environment compiled with support for GD (but this should already be in place)
* [Terrific Micro](http://namics.github.io/terrific-micro/) v1.0.0 or newer
* The files in your project extensions folder ;-)

        cd project/extensions
        git clone https://github.com/namics/php-spriter.git

## Usage

Include the spriter main file into your project (file: `project/index.project.php`)

    require_once(__DIR__ . '/extensions/php-spriter/spriter.inc.php');

... configure

    $spriterConf = array(
        "iconDirectory" => BASE . "project/resources/sprite/icon-sprite",      // directory, which contains your single icon files
        "cssDirectory" => "assets/css",                                        // where you want the sprite CSS to be saved. This folder has to be writable by your webserver.
        "spriteDirectory" => "assets/img",                                     // where you want the sprite image file to be saved. Folder has to be writable, too.
        "spriteFilename" => "icon-sprite",                                     // the name of the generated CSS and PNG file
        "retina" => array(2, 1),                                               // defines the desired retina dimensions, you want
        "retinaDelimiter" => "@",                                              // the delimiter inside the sprite image filename
        "cssFileExtension" => "css",                                           // the CSS file extension
        "namespace" => "icon-",                                                // the namespace for your icon CSS classes
        "ignoreHover" => false,                                                // set to true if you don't need hover icons
        "hoverSuffix" => "-hover"                                              // the name suffix for hovered icons.
    );

... and start

    new Spriter($spriterConf);

You can restrict the generation e.g. on page requests

    if (strpos($_SERVER['REQUEST_URI'], '.css') === false && strpos($_SERVER['REQUEST_URI'], '.js') === false) {
        new Spriter($spriterConf);
    }

It's also possible to generate multiple sprites

## Configuration

### Spriter Configuration

The required options should be self-explanatory.

### Templates

There are four templates using the files in `spriter/templates`:

    "globalTemplate" => "...",      // the global template, which contains general CSS styles for all icons
    "eachTemplate" => "...",        // the template for each CSS icon class
    "eachHoverTemplate" => "...",   // the template for each CSS icon hover class
    "ratioTemplate" => "...",       // the template for each retina media query

It's possible to use different template files.

    "globalTemplate" => file_get_contents(BASE . "project/extensions/php-spriter/spriter/templates/my-global.tpl"),

Please check [documentation](http://namics.github.io/php-spriter/) for default templates and placeholder names.

## More Infos

[Documentation](http://namics.github.io/php-spriter/)
