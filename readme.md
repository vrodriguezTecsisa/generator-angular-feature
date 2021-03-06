# AngularJS generator [![Build Status](https://secure.travis-ci.org/yeoman/generator-angular.png?branch=master)](http://travis-ci.org/yeoman/generator-angular) [![Built with Grunt](https://cdn.gruntjs.com/builtwith.png)](http://gruntjs.com/)

Maintainer: [Kamil Jastrzębski](https://github.com/codigo-pl)

Based on [generator-angular](https://github.com/yeoman/generator-angular/)

> Yeoman generator for AngularJS - lets you quickly set up a project with sensible defaults and best practises.

## Usage

Clone `generator-angular-feature` repository:
```
git clone https://github.com/codigo-pl/generator-angular-feature.git
```

`cd` into created directory and link generator:
```
cd generator-angular-feature && npm link
```

Make a new directory, and `cd` into it:
```
mkdir my-new-project && cd $_
```

Run `yo angular-feature:config` to generate a config file
```
yo angular-feature:config
```

Edit `config.json` file to customize paths and project structure
```
vim config.json
```

Run `yo angular-feature`, optionally passing an app name
```
yo angular-feature [app-name]
```

Run `grunt` for building and `grunt serve` for preview


## Generators

Available generators:

* [angular-feature:config](#config)
* [angular-feature](#app) (aka [angular-feature:app](#app))
* [angular-feature:controller](#controller)
* [angular-feature:directive](#directive)
* [angular-feature:filter](#filter)
* [angular-feature:route](#route)
* [angular-feature:service](#service)
* [angular-feature:provider](#service)
* [angular-feature:factory](#service)
* [angular-feature:value](#service)
* [angular-feature:constant](#service)
* [angular-feature:decorator](#decorator)
* [angular-feature:view](#view)

**Note: Generators are to be run from the root directory of your app.**

### Config
Creates a config file with choosen application structure in the root directory of your app.

Example:
```bash
yo angular-feature:config
```

Produces `config.json` (division by component):
```json
{
  "structure": {
    "type": "component",
    "app": {
      "path": "app",
      "assets": {
        "path": ""
      },
      "fonts": {
        "path": "fonts"
      },
      "images": {
        "path": "images"
      },
      "source": {
        "path": "scripts",
        "common": {
          "path": ""
        },
        "controller": {
          "path": "controllers"
        },
        "decorator": {
          "path": "decorators"
        },
        "directive": {
          "path": "directives"
        },
        "factory": {
          "path": "[service]"
        },
        "filter": {
          "path": "filters"
        },
        "provider": {
          "path": "[service]"
        },
        "service": {
          "path": "services"
        },
        "value": {
          "path": "[service]"
        }
      },
      "styles": {
        "path": "styles"
      },
      "vendor": {
        "path": ""
      },
      "view": {
        "path": "views"
      }
    },
    "test": {
      "path": "test"
    }
  }
}
```
or config.json (division by feature):
```json
{
  "structure": {
    "type": "feature",
    "app": {
      "path": "app",
      "source": {
        "path": "src",
        "common": {
          "path": "common"
        },
        "feature": {
          "path": "{{feature}}",
          "assets": {
            "path": "assets",
            "fonts": {
              "path": "fonts"
            },
            "images": {
              "path": "images"
            },
            "styles": {
              "path": "styles"
            }
          },
          "controller": {
            "path": "controllers"
          },
          "decorator": {
            "path": "decorators"
          },
          "directive": {
            "path": "directives"
          },
          "factory": {
            "path": "[service]"
          },
          "filter": {
            "path": "filters"
          },
          "provider": {
            "path": "[service]"
          },
          "service": {
            "path": "services"
          },
          "test": {
            "path": "tests"
          },
          "value": {
            "path": "[service]"
          },
          "view": {
            "path": "views"
          }
        }
      },
      "vendor": {
        "path": "vendor"
      }
    }
  }
}
```

Path value within a square brackets is a reference, e.g. path for 'factory' component will be 'services'.
Path value '{{feature}}' is replaced by a feature name during execution of subgenerator (e.g. angular-feature:controller) or by a 'common' value, when no feature is given.
Full path for the component is calculated based on nesting, e.g. 'app/src/{{feature}}/controllers' for a controller in a project divided by feature.

Example 1:
```bash
yo angular-feature:route foo/bar/myroute
```

Produces `app/src/foo/bar/controllers/myroute.js`:
```javascript
angular.module('myMod').controller('MyrouteCtrl', function ($scope) {
  // ...
});
```

Produces `app/src/foo/bar/views/myroute.html`:
```html
<p>This is the myroute view</p>
```

Example 2:
```bash
yo angular-feature:route myroute
```

Produces `app/src/common/controllers/myroute.js` and `app/src/common/views/myroute.html`.

### App
Sets up a new AngularJS app, generating all the boilerplate you need to get started. The app generator also optionally installs Twitter Bootstrap and additional AngularJS modules, such as angular-resource (installed by default).

Example:
```bash
yo angular-feature
```

### Route
Generates a controller and view, and configures a route in `app/scripts/app.js` connecting them.

Example:
```bash
yo angular-feature:route myroute
```

Produces `app/scripts/controllers/myroute.js`:
```javascript
angular.module('myMod').controller('MyrouteCtrl', function ($scope) {
  // ...
});
```

Produces `app/views/myroute.html`:
```html
<p>This is the myroute view</p>
```

### Controller
Generates a controller in `app/scripts/controllers`.

Example:
```bash
yo angular-feature:controller user
```

Produces `app/scripts/controllers/user.js`:
```javascript
angular.module('myMod').controller('UserCtrl', function ($scope) {
  // ...
});
```
### Directive
Generates a directive in `app/scripts/directives`.

Example:
```bash
yo angular-feature:directive myDirective
```

Produces `app/scripts/directives/myDirective.js`:
```javascript
angular.module('myMod').directive('myDirective', function () {
  return {
    template: '<div></div>',
    restrict: 'E',
    link: function postLink(scope, element, attrs) {
      element.text('this is the myDirective directive');
    }
  };
});
```

### Filter
Generates a filter in `app/scripts/filters`.

Example:
```bash
yo angular-feature:filter myFilter
```

Produces `app/scripts/filters/myFilter.js`:
```javascript
angular.module('myMod').filter('myFilter', function () {
  return function (input) {
    return 'myFilter filter:' + input;
  };
});
```

### View
Generates an HTML view file in `app/views`.

Example:
```bash
yo angular-feature:view user
```

Produces `app/views/user.html`:
```html
<p>This is the user view</p>
```

### Service
Generates an AngularJS service.

Example:
```bash
yo angular-feature:service myService
```

Produces `app/scripts/services/myService.js`:
```javascript
angular.module('myMod').service('myService', function () {
  // ...
});
```

You can also do `yo angular-feature:factory`, `yo angular-feature:provider`, `yo angular-feature:value`, and `yo angular-feature:constant` for other types of services.

### Decorator
Generates an AngularJS service decorator.

Example:
```bash
yo angular-feature:decorator serviceName
```

Produces `app/scripts/decorators/serviceNameDecorator.js`:
```javascript
angular.module('myMod').config(function ($provide) {
    $provide.decorator('serviceName', function ($delegate) {
      // ...
      return $delegate;
    });
  });
```

## Options
In general, these options can be applied to any generator, though they only affect generators that produce scripts.

### CoffeeScript
For generators that output scripts, the `--coffee` option will output CoffeeScript instead of JavaScript.

For example:
```bash
yo angular-feature:controller user --coffee
```

Produces `app/scripts/controller/user.coffee`:
```coffeescript
angular.module('myMod')
  .controller 'UserCtrl', ($scope) ->
```

A project can mix CoffeScript and JavaScript files.

To output JavaScript files, even if CoffeeScript files exist (the default is to output CoffeeScript files if the generator finds any in the project), use `--coffee=false`.

### Minification Safe

**Deprecated**

[Related Issue #452](https://github.com/yeoman/generator-angular/issues/452): This option is being removed in future versions of the generator. Initially it was needed as ngMin was not entirely stable. As it has matured, the need to keep separate versions of the script templates has led to extra complexity and maintenance of the generator. By removing these extra burdens, new features and bug fixes should be easier to implement. If you are dependent on this option, please take a look at ngMin and seriously consider implementing it in your own code. It will help reduce the amount of typing you have to do (and look through) as well as make your code cleaner to look at.


By default, generators produce unannotated code. Without annotations, AngularJS's DI system will break when minified. Typically, these annotations that make minification safe are added automatically at build-time, after application files are concatenated, but before they are minified. By providing the `--minsafe` option, the code generated will out-of-the-box be ready for minification. The trade-off is between amount of boilerplate, and build process complexity.

#### Example
```bash
yo angular-feature:controller user --minsafe
```

Produces `app/controller/user.js`:
```javascript
angular.module('myMod').controller('UserCtrl', ['$scope', function ($scope) {
  // ...
}]);
```

#### Background
Unannotated:
```javascript
angular.module('myMod').controller('MyCtrl', function ($scope, $http, myService) {
  // ...
});
```

Annotated:
```javascript
angular.module('myMod').controller('MyCtrl',
  ['$scope', '$http', 'myService', function ($scope, $http, myService) {

    // ...
  }]);
```

The annotations are important because minified code will rename variables, making it impossible for AngularJS to infer module names based solely on function parameters.

The recommended build process uses `ngmin`, a tool that automatically adds these annotations. However, if you'd rather not use `ngmin`, you have to add these annotations manually yourself. **One thing to note is that `ngmin` does not produce minsafe code for things that are not main level elements like controller, services, providers, etc.:
```javascript
resolve: {
  User: function(myService) {
    return MyService();
  }
}
```

will need to be manually done like so:
```javascript
resolve: {
  User: ['myService', function(myService) {
    return MyService();
  }]
}
```


### Add to Index
By default, new scripts are added to the index.html file. However, this may not always be suitable. Some use cases:

* Manually added to the file
* Auto-added by a 3rd party plugin
* Using this generator as a subgenerator

To skip adding them to the index, pass in the skip-add argument:
```bash
yo angular-feature:service serviceName --skip-add
```

## Bower Components

The following packages are always installed by the [app](#app) generator:

* angular
* angular-mocks
* angular-scenario


The following additional modules are available as components on bower, and installable via `bower install`:

* angular-cookies
* angular-loader
* angular-resource
* angular-sanitize

All of these can be updated with `bower update` as new versions of AngularJS are released.

## Configuration
Yeoman generated projects can be further tweaked according to your needs by modifying project files appropriately.

### Output
You can change the `app` directory by adding a `appPath` property to `bower.json`. For instance, if you wanted to easily integrate with Express.js, you could add the following:

```json
{
  "name": "yo-test",
  "version": "0.0.0",
  ...
  "appPath": "public"
}

```
This will cause Yeoman-generated client-side files to be placed in `public`.

## Testing

Running `grunt test` will run the unit tests with karma.

## Contribute

See the [contributing docs](https://github.com/yeoman/yeoman/blob/master/contributing.md)

When submitting an issue, please follow the [guidelines](https://github.com/yeoman/yeoman/blob/master/contributing.md#issue-submission). Especially important is to make sure Yeoman is up-to-date, and providing the command or commands that cause the issue.

When submitting a PR, make sure that the commit messages match the [AngularJS conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/).

When submitting a bugfix, write a test that exposes the bug and fails before applying your fix. Submit the test alongside the fix.

When submitting a new feature, add tests that cover the feature.

## License

[BSD license](http://opensource.org/licenses/bsd-license.php)
