# yo-profile [![NPM version][npm-image]][npm-url] [![Dependency Status][daviddm-image]][daviddm-url]
> Dynamic profile parser for Yeoman generators

Enable Yeoman generators to use static rc-type files for pre-populating (or overriding entirely) optional settings during project setup.

## Install

```sh
$ npm install --save yo-profile
```

## Generator Usage

Once installed, add an include for the project in your generator's base index file:

```js
var profile = new ( require( '../yo-profile' ).YoProfile );
```

Then, create an object, specifying default (empty) fields and a file path somewhere in your generator's `init` method. You can use chaining to immediately access the parsed properties:

```js
var Generator = yeoman.generators.Base.extend({
  init: function() {
    // ...
    
    var options = {
      'somesetting' : undefined,
      'othersetting': undefined
    };
    this.defaults = profile.load( options, 'mysettings' ).properties;
  }
})
```

The above snippet will attempt to load `.mysettingsrc` from your home directory or the directory of the project being created.

## CLI Usage

When invoking a yo-profile-powered generator, specify the desired profile with the `--profile` flag. For example:

```sh
yo generator:subgenerator --profile Boss
```

If no profile is specified, yo-profile will attempt to load the profile specified as the default.

## RC File Structure

By default, you should be using an INI file structure for your rc profile.

```sh
; The default profile will be used if no other profile is specified at runtime
default=First

[First]
  license   = MIT
  copyright = My Awesome Agency
  namespace = Magic
  php_min   = 7.0

[Second]
  license   = GPLv2+
  copyright = My Awesome Agency
  namespace = Magic
  php_min   = 5.2
```

## License

MIT © [Eric Mann](https://eamann.com)


[npm-image]: https://badge.fury.io/js/yo-profile.svg
[npm-url]: https://npmjs.org/package/yo-profile
[daviddm-image]: https://david-dm.org/ericmann/yo-profile.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/ericmann/yo-profile