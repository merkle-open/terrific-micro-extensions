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
        rm -rf php-spriter/.git

## Usage

Include the spriter main file into your project (file: `project/index.project.php`)

    require_once(__DIR__ . '/extensions/php-spriter/spriter.inc.php');

... configure

    $spriterConf = array(
        "forceGenerate" => false,                                              // set to true if you want to force the CSS and sprite generation.
    
        "srcDirectory" => BASE . "project/resources/sprite/icon-sprite",       // folder that contains the source pictures for the sprite
        "spriteDirectory" => BASE . "assets/img/sprite",                       // folder where you want the sprite CSS to be saved (folder has to be writable, too)
        
        "spriteFilepath" => "assets/img/sprite",                               // path to the sprite image for CSS rule
        "spriteFilename" => "icon-sprite",                                     // name of the generated CSS and PNG file.
        
        "tileMargin" => 4,                                                     // margin in px between tiles in the highest 'retina' dimension (default is 0) - if you generate different 'retina' dimensions, take a common multiple of the selected variants.
        "retina" => array(2, 1),                                               // defines the desired retina dimensions, you want.
        "retinaDelimiter" => "@",                                              // delimiter inside the sprite image filename.
        "namespace" => "icon-",                                                // namespace for your icon CSS classes
        
        "ignoreHover" => false,                                                // set to true if you don't need hover icons
        "hoverSuffix" => "-hover",                                             // set to any suffix you want.
        
        "targets" => array(
            // you can define multiple targets that will all reference the same png sprite
            array(
                "cssDirectory" =>  BASE . "assets/css",                        // folder where you want the sprite CSS to be saved (folder has to be writable, too)
                "cssFilename" => "icon-sprite.less",                           // your CSS/Less/Sass target file
                //"globalTemplate" => "...",                                   // global template, which contains general CSS styles for all icons (remove line for default)
                //"eachTemplate" => "...",                                     // template for each CSS icon class (remove line for default)
                //"eachHoverTemplate" => "...",                                // template for each CSS icon hover class (remove line for default)
                //"ratioTemplate" => "..."                                     // template for each retina media query (remove line for default)
            )
        )
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
