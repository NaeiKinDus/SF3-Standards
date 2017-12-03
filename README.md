# Symfony3 Custom PHP CodeSniffer Coding Standard

This is a fork of Endouble/Symfony3-custom-coding-standard
These are the Symfony2 standards, but tweaked to meet some needs we have in our CSB project, for example to comply with 
[PSR-12](https://github.com/php-fig/fig-standards/blob/master/proposed/extended-coding-style-guide.md) for PHP 7

## Installation - Linux

### Git clone

This standard can be simply cloned from github; this process allows using the standard system-wide.

a. Clone it from github to a local directory (ie. /opt/git/SF-Standards)

### Composer

This standard can also be installed with the [Composer](https://getcomposer.org/) dependency manager.

a. Add the repository to your composer.json: 
```json
 "repositories": [
        {
            "type": "vcs",
            "url": "git@github.com:NaeiKinDus/SF3-Standards"
        }
```

b. Add the coding standard as a dependency of your project

```json
 "require-dev": {
        "naeikindus/sf3-standards": "^1.0"
    },
```

## Installation - Windows



## Configuring PHPCS

1. Install PHP Code Sniffer like this:
    ```bash
    sudo curl -L https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar -o /usr/local/bin/phpcs && sudo chmod +x /usr/local/bin/phpcs
    ```

    Of course you can change the target directory where your phpcs binary will be; to do so, change the ```-o``` option of curl, and the chmod path.

2. Add the coding standard to the PHP_CodeSniffer install path

    The path should be the absolute path to this project's install path.
    ```bash
    sudo phpcs --config-set installed_paths <path_to_this_project_root_dir> // sudo is required if your PHPCS is installed in /usr/*
    ```

3. Check that the installed coding standards list "Symfony3Custom":
    ```bash
    phpcs -i
    ```

4. Done!
    ```bash
    phpcs --standard=Symfony3Custom /path/to/code
    ```
       
5. Set up PHPStorm / IntelliJ
    - configure code sniffer under File -> Settings -> Languages & Frameworks -> PHP -> Code Sniffer
      - in the configuration box, click on the "...", set the correct path to your phpcs binary then click on validate
      - if validating raises an error, fix it.
    - Go to Editor -> Inspections -> PHP -> PHP Code sniffer validation, click on the checkbox to enabled it then
        refresh the standards and select Symfony3Custom

6. Customize PHPCS *(optional)*
    - ```phpcs --config-set colors 1``` to enable colored output
    - ```phpcs --config-set default_standard Symfony3Custom``` to set this project's rule as the default one

## Customizations

The following adjustments have been made to the original standard:

In Sniff/WhiteSpace/AssignmentSpacingSniff:
- Added an exception for ```declare(strict_types=1);``` to comply with [PSR-12](https://github.com/php-fig/fig-standards/blob/master/proposed/extended-coding-style-guide.md#3-declare-statements-namespace-and-use-declarations) 

In Sniff/WhiteSpace/FunctionalClosingBraceSniff:
- copied from Squiz and adapted to have no blank line at the end of a function

In Sniff/Commenting/FunctionCommentSniff:
- check for 1 blank line above a docblock
- don't check docblocks for test and setUp methods (PHPunit, would be blank)
- do check protected and private methods for docblocks

In Sniff/NamingConventions/ValidClassNameSniff
- remove the abstract class name rule

In ruleset.xml
- Disabled the class comment rule
- Changed the concatenation spacing rule, for readability, to require 1 space around concatenation dot, instead of no spaces as the [Symfony](https://symfony.com/doc/current/contributing/code/standards.html#structure) standard requires.
- Re-enabled the blank line check from superfluousWhitespace (disabled in PSR-2)
