UN3 Base Theme
==============

This is a base theme for UN projects.

This theme is designed using the following style guide: https://xd.adobe.com/view/9677519d-1a44-46d6-b293-1d3785866302-c324/grid/

This theme is based on [Barrio](https://www.drupal.org/project/bootstrap_barrio) theme, which is built upon [Bootstrap 5](https://getbootstrap.com/).

This theme is build using [Barrio SASS Starter Kit](https://www.drupal.org/project/bootstrap_sass) according to the [documentation](https://www.drupal.org/docs/contributed-themes/bootstrap-45-barrio-sass-starter-kit/installation).



1. Installation
---------------

1.1. Prior installing the base theme you need to update your composer.json to according the following instructions: https://www.drupal.org/docs/develop/using-composer/manage-dependencies#third-party-libraries (Downloading third-party libraries using Composer section of the Using Composer to Install Drupal and Manage Dependencies documentation).

To configure the source repositories, then add the following lines in your project's root composer.json:
```
    "repositories": [
        {
            "type": "composer",
            "url": "https://packages.drupal.org/8"
        },
        {
            "type": "composer",
            "url": "https://asset-packagist.org"
        },
        {
            "type": "package",
            "package": {
                "name": "undpi/un3-base-theme",
                "version": "1.0",
                "type": "drupal-un3-custom-theme",
                "source": {
                    "url": "git@bitbucket.org:undpi/un-3-base-theme.git",
                    "type": "git",
                    "reference": "develop"
                },
                "require": {
                    "bower-asset/fontawesome": "^6.4",
                    "npm-asset/swiper": "^8",
                    "drupal/bootstrap_barrio": "*",
                    "bower-asset/fontawesome-iconpicker": "^3.2",
                    "drupal/fontawesome_menu_icons": "^2.0",
                    "drupal/simple_search_form": "^1.5",
                    "drupal/colorpalette": "^1.0",
                    "drupal/entity_form_field_label": "^1.7",
                    "drupal/text_field_formatter": "^2.0",
                    "drupal/bootstrap_layout_builder": "^2.1"
                },
                "require-dev": {
                    "drupal/bootstrap_saas": "*"
                }
            }
        }
    ],
```
There is also a pending configuration to install all dependencies to proper destination. For this, we will need to install oomphinc/composer-installers-extender:

`composer require oomphinc/composer-installers-extender`

Then we will be able to configure `installer-paths`. The idea is to have something similiar to this:
```
    "extra": {
        "installer-types": [
            "drupal-un3-custom-theme",
            "npm-asset",
            "bower-asset"
        ],
        "installer-paths": {
            ...

            "web/libraries/{$name}": [
                "type:drupal-library",
                "type:npm-asset",
                "type:bower-asset"
            ],

            ...

            "web/themes/custom/un3": [
                "type:drupal-un3-custom-theme"
            ]
        },
```


Then run `composer require undpi/un3-base-theme`.

This theme already contains compiled CSS and JS files, so it's not needed to re-compile them to start using this theme, just enable it in the Drupal.

1.2. For development purposes, it's required to have node.js, npm and gulp installed.

First, you need to install node.js packages from the supplied with the theme `package.json` and `package-lock.json` using the following command:

	npm install

Then update the following part of the `gulpfile.js` file with your own domain:

	browserSync.init({
	  proxy: "http://yourdomain.com",
	});

Then just run the following command:

	gulp

If everything is installed and configured properly, then a new browser window should be opened with the website, and the `Browsersync: connected` message should appear in the top right corner of the browser window.

If you need just to compile all CSS files without running watcher and Browsersync, please run the following command:

	gulp build



2. Using Starter Kit
--------------------

There is a special cloned version of the [Barrio SASS Starter Kit](https://www.drupal.org/project/bootstrap_sass) called `un3_start`.
It's not a real theme, it just a template for creation of the themes based on the UN3 Base Theme.
To create a subtheme of UN3 Base Theme for the Drupal UN project, first run the following command from the root of the `un3_start` folder:

	bash scripts/create_subtheme.sh

The script will ask a series of configuration questions and then create the subtheme in the `web/themes/custom` folder of the project (in the parent repository, not in the current).
Then you need to follow all the steps from the **1.2** section of this Readme to start working with the new theme.
