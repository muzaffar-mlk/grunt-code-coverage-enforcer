# grunt-code-coverage-enforcer

> Enforces code coverage thresholds for a project with lcov files. This means it works with a wide range of code coverage tools like blanketjs, istanbul, .....

## Introduction

Most code coverage enforcers are tied to a specific code coverage tool like blanketjs or istanbul.
This plugin works on the lcov file that can be generated by most test runners.

As a result you can work with any tests runners that are capable of generating the widely used LCOV file format.

## Why is our plugin better

Most other coverage threshold tools fail the build only when you have a test and the test doesn't meet the threshold criteria.  **Most tools will actually pass the build if you dont write any tests for your project**.

This plugin will check and fail if there are files that have not been covered at all.

----

## Getting Started

```shell
npm install grunt-code-coverage-enforcer --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-code-coverage-enforcer');
```

## The "code-coverage-enforcer" task

## You will need to enable lcov reporter in your test runner.

Sample Intern config
```js
intern:  {
   runner: {
        options: {
            config: "<intern- config>",
            runType: "runner",
            reporters: ["console", "lcov"]
        }
    }
  }
```

This should typically generate an lcov.info file that will specified as input into the code-coverage-enforcer plugin.


### Overview
In your project's Gruntfile, add a section named `code-coverage-enforcer` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  code-coverage-enforcer: {
    options: {
        lcovfile: "lcov.info",
        lines: 60,
        functions: 60,
        branches: 60,
        src: "src",
        includes: ["src/**/*.js"],
        excludes: ["src/uncoveredfile.js"]
    }
  },
})
```

the default threshold values are 
```js
          {
            lines: 50,
            functions: 50,
            branches: 0,
            includes: ["**/*.js"],
            src: process.cwd(),
            excludes: []
        }
```

### Options

#### lines
Type: `Number`
Default value: `50`

A Number value that is used to specify in % the line coverage required.

#### functions
Type: `Number`
Default value: `50`

A Number value that is used to specify in % the function coverage required.

#### branches
Type: `Number`
Default value: `50`

A Number value that is used to specify in % the branches coverage required.

#### src
Type: `string`
Default value: `src`

The location of the folder within which we will search for files.

#### includes
Type: `matcher`
Default value: `*`

The matcher required to compare files within the src location that are to be included


#### includes
Type: `[matcher]`
Default value: `[]`

The matchers required to compare files within the src location that are to be excluded.




### Usage Examples

#### Default Options
In this example, the default options are used 

```js
grunt.initConfig({
  code-coverage-enforcer: {
    options: {
        lcovfile: "lcov.info",
        includes: ["src/**/*.js"],
        excludes: ["src/uncoveredfile.js"]
    }
  },
})
```

#### Custom Options
In this example, custom options are used to specify the threshold limits
```js
grunt.initConfig({
  code-coverage-enforcer: {
    options: {
        lcovfile: "lcov.info",
        lines: 60,
        functions: 60,
        branches: 60,
        src: "src",
        includes: ["src/**/*.js"],
        excludes: ["src/uncoveredfile.js"]
    }
  },
})
```


### Recommendations

We recommend using a specific task names build acceptance that will run the code-coverage-enforcer along with other build acceptance type of tasks.

Here is an example config that should go into your Gruntfile 
```js

    grunt.registerTask("build-acceptance", ["code-coverage-enforcer"]);
```

You can now simply invoke this from command line using

> grunt build-acceptance

## Contributing
The project includes jshint and jscs config as part of its dev grunt tasks. Please run grunt lint to ensure that the code passes the code conventions.

## Release History
June 19 2014
Initial Release.

## License
Copyright (c) 2014 Intuit. Licensed under the MIT license.