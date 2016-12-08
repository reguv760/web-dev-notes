# WordPress Notes

* [part 1](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-1.md)
* [part 2](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-2.md)
* [part 3](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-3.md)
* [part 4](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-4.md)
* [part 5](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-5.md
# WordPress - Building a Custom Theme

<<<<<<< 7637fb5132baa5061aa22390681d76d9b17492aa
There are two ways to install WordPress. The traditional (long way) and the WP-CLI (short way). Obviously, the shorter, the better but let's just show you the long way for thoroughness.

## [The Traditional Way to Install WordPress](how-to-install-wordpress.md)
* We assume you are using MAMP
* Other Dev Server Setups
    - XAMPP
    - WAMP
    - Desktop Server
    - VVV, Virtual Box and Vagrant

## Install WordPress Using WP-CLI (recommended)

Use my WP-CLI notes for install instructions (or use the [WP-CLI page](http://wp-cli.org/) for easy to follow instructions)

This will grab all the current WordPress files from the github WordPress repo, extract them and put them inside your site project folder. This is a huge time saver as it can install WordPress in seconds (with a fast internet connection)

```
$ wp core download
```

### Create the wp-config.php file

If you were manually installing WordPress through the browser you would be brought to a page where you put in your database connection information. This would in turn create your `wp_config.php` file. WP-CLI speeds this step up with a little terminal magic.

Before you do this step you need to create a database in MySQL. Using the GUI phpMyAdmin is the way most people do this. You can also use the Terminal, sign into MySQL and create a database this way. As you use the terminal more and more the second option may become your first choice.

So now you are ready to create your `wp-config.php` file

```
$ wp core config --dbuser=root --dbpass=root --dbname=stranger_things_wp
```

This will create the file to connect you to your MySQL databse. The above code is assuming you used MAMP and the default username and password for MAMP is root and root. Change the --dbname value to match the name you used when creating the empty database in phpMyAdmin (or MySQL terminal). I recommend using underscores instead of dashes in db names with more than one word (ie my_db instead of my-db). For security reasons you may want to not have db in name so hackers won't find it so easily.

### Finishing Up Core Install

If you were manually installing WordPress through the browser you would be brought to a page asking you for your username and password, title of the page, email and URL of your WordPress site (local, staging or production depending on the environment you are working in). WP-CLI speeds this step up with the magic of the terminal.

```
$  wp core install --url=http://localhost/stranger-things --title=StrangerThings --admin_user=admin --admin_password=password --admin_email=howley.phil@gmail.com
```

## Bootstrap
For this project we will use Bootstrap 4. It is currently the most popular framework. The great thing is it gives you responsiveness and grid layouts right out of the box.

### Download Bootstrap
[Download Bootstrap](http://getbootstrap.com/getting-started/)

First we are now going to use bootstrap 4 (instead of bootstrap 3)
We are also going to install with node and it's npm (node package manager). This is way faster than manually downloading it.

### Where will our custom theme be located?
In the themes folder `wp-content/themes`

So create your custom theme inside this `themes` folder. For the sake of this example, let's call it `thunder-tube-theme`.

`$ mkdir wp-content/themes/thunder-tube-theme`

Change into that directory

`$ cd wp-content/themems/thunder-tube-theme`

This is the folder you need to be inside because this is where all your custom theme stuff goes.

## Get Git!
Inside your theme you need to start listening with Git (and add version control to your theme)

`$ git init`

### Which text editor do you currently recommend?
I like Atom. I have used Sublime Text for years and find Atom to be a superior product.

But I do find Atom slow at times and I jump back to Sublime Text from time-to-time.

### Create `package.json` in the root of your custom theme

`$ npm init -y`

**note** the `-y` flag is a way to save you from answering all the questions npm usually asks you when it creates `package.json`.

### Grab Bootstrap 4

**note** This code may change so this is the site where you can the most updated `npm` code.

`$ npm install bootstrap@4.0.0-alpha.5 --save`

**note** the `--save` flag saves this to your `package.json`

Bootstrap 4 requires the `tether` and `jquery` dependencies

You don't need to grab jquery because it comes bundled with WordPress.

`$ npm install tether --save`

Check out your `package.json` and you should see bootstrap 4 and tether are now listed in the `dependencies` portion of the JSON file.

## Sample package.json

After installing bootstrap and saving it, `package.json` will look something like this:

```js
{
    "name": "thunder-tube-theme",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "peh2",
    "license": "ISC",
    "dependencies": {
        "bootstrap": "^4.0.0-alpha.5",
        "tether": "^1.3.7"
    }
}
```

## Add these files to your custom theme folder

Custom themes can have lots of files. But the only required files are `index.php` and `style.css`.

* functions.php
* header.php
* footer.php
* index.php (required)
* style.css (required)

## Add with Git

First check your site with `$ git status`

You will see `node_modules` and that we are tracking it. We don't want to as this code we never edit because it's 3rd party code. We use it but it is not ours so therefore we don't need to add it to our git repo. If we added `node_modules` to all our repos, we would waste space needlessly. Give a hoot. Don't pollute! `:)`

### .gitignore

This file will allow git to ignore `node_modules`

Add it to the root of your custom theme.

`$ touch .gitignore`

And add `node_modules` to that file. You can do that through the terminal with:

`$ echo "node_modules" >> .gitignore`

Save and check the status with

`$ git status`

And you will see `node_modules` is no longer being watched by git.

#### Now we are ready to add our new stuff to gits staging area.

`$ git add -A`

## Commit with Git

`$ git commit -m 'initialize repo'`

## Never work in the master branch

The master branch is for your production code.

Whenever you are working on a new feature you should create a feature branch.

## Create a feature branch

`$ git checkout -b my-first-feature-branch`

Now you just created a new branch named `my-first-feature-branch` and switched into it (that's what the -b flag did)

This branch has everything the master branch had but you now can add new stuff without worrying it will mess up the master branch.

Let's add a background color to our site.

`style.css`

```css
body {
  background-color: red;
}
```

Save and commit.

`$ git add style.css`

`$ git commit -m 'add background color'`

## Switch back to the master branch
`$ git checkout master`

Notice how we don't see our new style in the master branch? This is because branches don't see each other. They are self contained. When you create a branch, it takes a copy of the branch you are in and puts it inside the new branch.

## Merge Branch
We want to take the code we had in our `my-first-feature-branch` branch and merge it into the master branch. We can do that with:

`$ git merge my-first-feature-branch`

Now the master branch will have the new body background.

I won't keep adding branches in my notes but you should get into this habit. Never work with new stuff in the master branch. Create a new branch and when you know it works and it is what you want. Add, commit and switch back to the master branch and merge your changes.

## Add images with Terminal
In the root of every WordPress custom theme you need an image named `screenshot.png`. This image is what will be used to show a snapshot of what your custom theme looks like.

**Question**

_Can we grab images from the internet directly from the internet?_

Heck yes!

Use this code to grab a proper dimensioned `screenshot.png` to give you a cute example of how to add a `screenshot.png` using the terminal

* Make sure you are inside the custom theme folder when entering this code

```
$ curl -O https://make.wordpress.org/training/files/2013/10/screenshot.png
```

You now have `screenshot.png` inside your theme and WordPress will use this to show a screenshot of your theme. You are supposed to take a screenshot of your finished theme. The dimensions of the image you add are the recommended dimensions for all your screenshots.

## Add special css comment to style.css

Some may find this strange but WordPress using comments to give itself special instructions. The `style.css` file is a perfect example of this. Here you see a comment that adds meta information about the theme to the Dashboard. You can put all your CSS in this file but there is a better way to break up your CSS with help from the `functions.php` file.

Add the following comment code to the top of `style.css`. It is important to name it `style.css`. If you name it something different like `styles.css` you will break your theme.

```css
/*
Theme Name: Kingluddite Magazine Theme
Author: Kingluddite
Author URI: http://kingluddite.com/
Description: A simple theme to showcase how to build a theme from Twitter Bootstrap
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Code and take over the world line-by-line
*/
```

## Activate Your Theme

So if you are logged into your WordPress Dashboard and you navigation to `Appearance > Themes` you should see your theme. If you don't you may have created a `broken theme` and you'll have to troubleshoot to get it working. WordPress usually will give you a broken theme notice and let you know what the problem may be. If you added a screenshot.png to your theme, you will see that image in the themes page of your Dashboard. Click Activate and your theme will now be live. Click `Visit Site` in Dashboard to view your live site. Don't get too excited because it will blank.

## A Better way to activate your theme using WP-CLI

`$ wp themes activate thunder-tube-theme`

## Our Bootstrap 4 Starter Template

We'll use this template and convert it so it looks the same in our WordPress custom theme.

[Our BS template](http://v4-alpha.getbootstrap.com/examples/jumbotron/)

* View the page in Chrome and view the source of the page. Copy the source and paste it into `index.php`. The CSS won't be working but you will see the content.

## Break up our page into pieces

### header.php

In `index.php`, select from the `<!DOCTYPE html>` down to the closing `</nav>` element and paste inside `header.php`

### php includes

#### get_header()

If you worked with PHP before you know about includes. It's just a way to include a chunk of code onto another page. `get_header()` will pull into index.php the code inside `header.php`.

Replace the cut code in `index.php` with the following PHP code:

`index.php`

```php
<?php get_header(); ?>
[rest of index.php code here]
```

View page in browser to test if header include is working

#### get_footer()

In `index.php` select and cut from the HR element to end of the HTML element and paste into `footer.php`.

Replace cut code in `index.php` with the following PHP code:

```php
[rest of index.php code here]
<?php get_footer(); ?>
```

View page in browser to test if `footer.php` include is working

## Proper Way to Include CSS in WordPress

In a static HTML page, you use LINK elements to point to the CSS files. In WordPress the proper (and secure) way to include CSS is through the `functions.php` page.

Add this to `functions.php`

`functions.php`

```php
<?php
function theme_styles() {
    wp_enqueue_style( 'bootstrap_css', get_template_directory_uri() . '/node_modules/bootstrap/dist/css/bootstrap.min.css' );
}
add_action( 'wp_enqueue_scripts', 'theme_styles' );
?>
```

## Hooks in WordPress

There will be times where you need to inject code at a certain part of your custom theme. That is where hooks come in. In a standard static HTML site, you would put LINK elements to point to your CSS. In WordPress we use the `wp_head()` **hook** to inject the CSS we have line up (or a better WordPress word to use here would be **enqueued**). Once you do this and view your WordPress site, you will see that the CSS from Twitter Bootstrap's Jumbo sample page is now working.

In `header.php` add this php to just before closing HEAD element

```php
<?php wp_head(); ?>
</head>
```

## View Source Code

### 404 Errors

Right click on the page and `View Page Source`. This will let you see if the hook is working. Our Bootstrap Jumbotron code still has some static links. Check out all these broken 404 pages. It means we requested the page from the server and the server tells us that it has no idea what we are talking about because the files we requested do not exist on the server.

Here are some 404 errors when we use the Console in Google Chrome (shortcut to open is `cmd`+`option`+`j`)

![404 errors](https://i.imgur.com/6RW0uHc.png)

You will see that `bootstrap.min.css` is included
![our hook is working](https://i.imgur.com/3jC4etb.png)

* Delete unused old link to `bootstrap.min.css`

## Add our style.css using our functions.php page
What about link to `jumbotron.css`? How can we add that?

On the original static source if you click on the link it will take you to jumbotron.css and show you this code:

```css
body {
  padding-bottom: 2rem;
}
```

Copy that code and put it at the bottom of `style.css`

To enqueue it (add it to our list of needed css files) just adjust our `functions.php` file to look like the following:

```php
/* add css */
function theme_styles() {
    wp_enqueue_style( 'bootstrap_css', get_template_directory_uri() . '/node_modules/bootstrap/dist/css/bootstrap.min.css' );
    wp_enqueue_style( 'jumbotron_css', get_template_directory_uri() . '/css/jumbotron.css' );
    wp_enqueue_style( 'main_css', get_template_directory_uri() . '/style.css' );
}
add_action( 'wp_enqueue_scripts', 'theme_styles' );
?>
```

Above shows you how we can point to our node_modules version of bootstrap 4, as well as a custom css file `jumbotron.css` and we also can point to the style.css file located in the root of our WordPress theme. Now you know how to include any time of css inside WordPress.

You can now delete the `hardcoded` link tag inside your `header.php` file that points to `jumbotron.css`



```html
    <!-- Custom styles for this template -->
    <link href="jumbotron.css" rel="stylesheet">
```

#### wp_enqueue_style('name', path to file)

The first parameter is just an internal name WordPress uses
The second parameter concatenates a cool `get_template_directory_uri()` function that has the ability to point us the active theme and then we concatenate the rest of the path from inside the custom theme folder.

If you view the source you should now see that our custom theme `style.css` file is now there:

![style.css in source code](https://i.imgur.com/9QSoFEG.png)

**Important** WordPress has jQuery built in

## Adding JavaScript files using functions.php

`functions.php`

You'll see this is very similar to what we did with CSS but here we use the `wp_enqueue_script` which has a few different parameters

### Important parameters in wp_enqueue_script()
* The 3rd parameter allows us to include dependencies this JavaScript file needs. It can just be one file (like jQuery) or more than one file.
* The last parameter is boolean which enable you to have the JavaScript file in the HEAD element of our `header.php` (false) or in the footer.php file just before the closing `</body>` tag (true).

```php
<?
/* our css enqueues here (the code we did before) */

/* add JavaScript */
function theme_js() {
    wp_enqueue_script( 'bootstrap_js', get_template_directory_uri() . '/node_modules/bootstrap/dist/js/bootstrap.min.js', array('jquery, tether'), '', true );
    wp_enqueue_script( 'ie10_js', get_template_directory_uri() . '/js/ie10-viewport-bug-workaround.js', array('jquery'), '', true );
}
add_action( 'wp_enqueue_scripts', 'theme_js' );
?>
```

## Another hook - wp_footer()

View source and you won't see included `bootstrap.min.js` in footer
because you forgot to include the footer hook

`footer.php`

```php
[more code here]
<?php wp_footer(); ?>

 </body>
</html>
```

### Delete JavaScript static code located in `footer.php`

**note** your code may be slightly different but just make sure you delete any hardcoded links to JavaScript.

```html
 <!-- Bootstrap core JavaScript
    ================================================== -->
    <!-- Placed at the end of the document so the pages load faster -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script>window.jQuery || document.write('<script src="../../assets/js/vendor/jquery.min.js"><\/script>')</script>
    <script src="../../dist/js/bootstrap.min.js"></script>
    <!-- IE10 viewport hack for Surface/desktop Windows 8 bug -->
    <script src="../../assets/js/ie10-viewport-bug-workaround.js"></script>
```

### Add a `js` folder inside your theme

**Note** I create a new file inside `js` with the ie10 fix

```
$ touch js/ie10-viewport-bug-workaround.js
```

`js/ie10-viewport-bug-workaround.js`

```js
/*!
 * IE10 viewport hack for Surface/desktop Windows 8 bug
 * Copyright 2014-2015 The Bootstrap Authors
 * Copyright 2014-2015 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */

// See the Getting Started docs for more information:
// https://getbootstrap.com/getting-started/#support-ie10-width

(function () {
  'use strict';

  if (navigator.userAgent.match(/IEMobile\/10\.0/)) {
    var msViewportStyle = document.createElement('style')
    msViewportStyle.appendChild(
      document.createTextNode(
        '@-ms-viewport{width:auto!important}'
      )
    )
    document.head.appendChild(msViewportStyle)
  }

})();
```

## WordPress filters

### Hide admin bar

Sometimes when you are logged in, the WordPress Admin CSS gets in your way. You have the ability to override it.

`functions.php`

```php
add_filter( 'show_admin_bar', '__return_false' );
```

This is a simple filter that hides the admin bar

## 20. WordPress body_class()

This is a very powerful dynamic function that generates a bunch of classes inside the BODY element. You can use these classes to style a WordPress page the way you want depending on the situation.

`header.php`

If you add the following code and then view the source code, you'll see a bunch of classes have been added to the body.

```php
<body <?php body_class(); ?>>
<!-- rest of code -->
```

![body class php function output](https://i.imgur.com/5SljR6O.png)

### Push down the admin bar when logged in

`style.css`

Add this underneath our existing code

```css
.admin-bar .navbar-fixed-top {
    margin-top: 30px;
}
```

## Menus (new)

You can add a menu using the dashboard. It involves multiple steps. You need to add your menu items. Create a new menu, name it and save it. Then you need to point to the location of where the menu you will go.

But a much [easier way](https://wp-cli.org/commands/menu/) it to use WP-CLI

```
# Create a new menu
$ wp menu create "Primary"
Success: Created menu 200.

# List existing menus
$ wp menu list
+---------+----------+----------+-----------+-------+
| term_id | name     | slug     | locations | count |
+---------+----------+----------+-----------+-------+
| 177     | Primary  | primary  | primary   | 7     |
+---------+----------+----------+-----------+-------+

# Create a new menu link item
$ wp menu item add-custom my-menu Apple http://apple.com --porcelain
1922

# Assign the 'my-menu' menu to the 'primary' location
$ wp menu location assign my-menu primary
Success: Assigned location to menu.
```

### The Walker Class

This part is in a little transition because the walker class was for Bootstrap 3 and we need to find code that was updated to Bootstrap 4. [A developer forked](https://github.com/sebakerckhof/wp-bootstrap-navwalker/blob/580e114965778a495464c6755a202c07cdbbb58d/README.md) the code and updated it but the pull request has yet to be merged.

[Here is the current code](https://github.com/sebakerckhof/wp-bootstrap-navwalker/blob/580e114965778a495464c6755a202c07cdbbb58d/wp_bootstrap_navwalker.php). Create a file called `wp_bootstrap_navwalker.php` and add the current code to it.

`functions.php`

* add this code to the top of your functions.php

```php
<?php
// Register Custom Navigation Walker
require_once('wp_bootstrap_navwalker.php');
/* menus */
add_theme_support( 'menus' );
function register_theme_menus() {
    register_nav_menus(
      array(
        'primary' => __( 'Primary', 'thunder-tube-theme' )
      )
    );
}
add_action( 'init', 'register_theme_menus' );
/* add css */
```

### Create 3 pages in Dashboard

We'll create these pages but we won't be able to view them. The reason is because of WordPress' hierarchy. But we will at least be able to get our menu to work.

* Home
* Sample Page
* Blog

note: delete the Home page with a custom link in the WordPress Admin `Menus` section

![Menu Dashboard](https://i.imgur.com/LtUqqox.png)

## WordPress bloginfo()
In Dashboard, Menus, Create menu, choose Header Menu as theme location
in source code change blog name `header.php` to

```
...<a class="navbar-brand" href="<?php bloginfo( 'url'); ?>"><?php bloginfo( 'name'); ?></a>...
```

# Menu's in WordPress
You have choices when making menus. You can do it the simpleway for a basic Menu that is built on your existing pages in WordPress. Or you can create a custom menu that only shows certain pages that you choose. You also need to select a location. Or you can create a complex navigation using Twitter Bootstrap with the Walker class.

Lete's start with a simple menu.

## Simple Menu
This is a three step process.

1. Create your pages in WordPress that you want to be in your navigation. Let's say for the sake of simplicity. You create three pages home, about, contact.
2. Add this code to your `functions.php`

```php
/*=============================
=            Menus            =
=============================*/
add_theme_support( 'menus' );
function domsters_register_menu() {
  register_nav_menu('main-menu', __( 'Main Menu') );
}
add_action('init', 'domsters_register_menu');
```

3. In the WP Dashboard, you select `Menus`
4. Create a New Menu by clicking `create a new menu`. Give it a name. Let's call it 'Primary'. Drag and drop your pages to your new `Primary` window. Then click `Save Menu`
5. Choose the location by selecing the `Main Menu`
6. Add your navigation to your code. For my simple navigation, I am adding it to the `header.php`. So drop this code inside `header.php`

**note** you may have to change some of the values of the array properties depending on the structure of your navigation.

`header.php`

```php
  <?php
  $defaults = array(
    'theme_location'  => 'main-menu',
    'menu'            => '',
    'container'       => 'nav',
    'container_class' => '',
    'container_id'    => '',
    'menu_class'      => 'main-nav',
    'menu_id'         => '',
    'echo'            => true,
    'fallback_cb'     => 'wp_page_menu',
    'before'          => '',
    'after'           => '',
    'link_before'     => '',
    'link_after'      => '',
    'items_wrap'      => '<ul id="%1$s" class="%2$s">%3$s</ul>',
    'depth'           => 0,
    'walker'          => ''
  );
  wp_nav_menu( $defaults );
   ?>
```

### The Walker Class
If you want to try and tackle the Bootstrap 4 navigation follow these instructions:

### Add your menu to your site page


## wp_nav_menu()

`header.php`

```php
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
    <meta name="description" content="">
    <meta name="author" content="">
    <link rel="icon" href="../../favicon.ico">

    <title>Jumbotron Template for Bootstrap</title>

    <?php wp_head(); ?>
  </head>

  <body <?php body_class(); ?>>


      <a class="navbar-brand" href="#">Project name</a>
      <?php
            wp_nav_menu( array(
                'menu'              => 'primary',
                'theme_location'    => 'primary',
                'depth'             => 2,
                'container'         => 'nav',
                'container_class'   => 'navbar navbar-static-top navbar-dark bg-inverse',
        'container_id'      => 'bs-example-navbar-collapse-1',
                'menu_class'        => 'nav navbar-nav',
                'fallback_cb'       => 'wp_bootstrap_navwalker::fallback',
                'walker'            => new wp_bootstrap_navwalker())
            );
        ?>
```

* check out [wp_nav_menu()](https://developer.wordpress.org/reference/functions/wp_nav_menu/) on codex
* check out and see pages are showing on nav
* set front page as Home and Blog as Blog page

`style.css`

This will highlight the currently selected page in WordPress. Twitter bootstrap uses different CSS for an active page and this shows you how to alter this code using what class WordPress uses for the current page.

```css
.current-menu-item > a {
    background: #000;
}
```

## Permalinks

This a great feature of WordPress that will greatly improve your SEO with just a few clicks. It makes your URL much more SEO friendly.

* How to change them in the Dashboard
* Improves SEO

Before Permalinks

![Before Permalinks](https://i.imgur.com/zukfE79.png)

After Permalinks

![After Permalinks](https://i.imgur.com/gRCsfkk.png)

## 26. Install Bootstrap Shortcodes
* [link](https://wordpress.org/plugins/bootstrap-shortcodes/)
* Kevin Attfield
* Install and Activate
* view page and you'll see shortcodes in editor

## 27. Add Google Fonts

Add this to `functions.php`

`functions.php`

```php
// activate google fonts
function tutsplus_add_google_fonts() {
  wp_register_style( 'googleFonts', 'http://fonts.googleapis.com/css?family=Open+Sans:400,300');
  wp_enqueue_style( 'googleFonts');
}
add_action( 'wp_enqueue_scripts', 'tutsplus_add_google_fonts' );
```

And here is an example of using it in `style.css`

`style.css`

```css
/* Headings */
h1, h2, h3, h4, .site-name {
  font-family: 'Open Sans', sans-serif;
}
```

# WordPress Notes

* [part 1](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-1.md)
* [part 2](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-2.md)
* [part 3](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-3.md)
* [part 4](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-4.md)
* [part 5](https://github.com/kingluddite/web-dev-notes/blob/master/cms/wordpress/bootstrap-wordpress-part-5.md)