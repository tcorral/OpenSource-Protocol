# OpenSource Protocol

##Signup in Github:

##Login in Github:

* Log in [Github](https://github.com/login)

##Create a Repository:

* Log in [Github](https://github.com/login)
* Open [Github](https://github.com/new)
* Give a name
* Give a description
* Select privacy to Public
* Check 'Initialize this repository with a README'
* Open the 'Add a license' dropdown and select the license you want.
    * I recommend you to use MIT License to allow commercial and non profit usage.
* Your repository should be initialized with these two files:
    * README.md
    * LICENSE


##Create a Javascript project:
* Add Travis to your project
    * Open [Travis](https://travis-ci.org/)
    * In the top bar to the right, select 'Start with Github'
        * Insert your credentials if needed.
        * You will get an account in Travis.
            * The user will be the same as it's in Github
            * Travis creates a token for you, see your profile, take note because it will be asked to you in Github to configure Travis hook.
        * Below your avatar select 'Accounts' link to see your repositories
        * Search your project in the list
        * Click in the off switch to change it to on.
    * Come back to Github
    * Open your project settings

        https://github.com/USER/PROJECT_NAME/settings

    * Select 'Service hooks' in left menu
    * Search Travis
    * Click on Travis
    * Insert your user
    * Insert the token you got in Travis profile page.
    * Left Domain in blank
    * Check Active checkbox.
* Create a .gitignore folder in root with this content

        .node_modules/*
        .coverage/*

    * If you use PHPStorm you should add the next line:

        .idea/*

* Create a src folder in root.
* Create a test folder in root.
* Create a versions folder in root.
* Create a package.json in root.

        {
          "name": "PROJECT_NAME",
          "version": "X.X.X",
          "description": "DESCRIPTION,
          "homepage": "WEB PAGE OF YOUR PROJECT",
          "author": "YOUR FULL NAME",
          "main": "./src/MAIN_FILE.js",
          "keywords": [
            "KEYWORDS TO INDEX YOUR PROJECT"
          ],
          "licenses": [
            {
              "type": "LICENSE_TYPE",
              "url": "http://www.opensource.org/licenses/LICENSE_TYPE-license.php"
            }
          ],
          "bugs": {
            "mail": "YOUR_EMAIL@MAIL_DOMAIN",
            "url": "https://github.com/USER/PROJECT/issues"
          },
          "repository": {
            "type": "git",
            "url": "https://github.com/USER/PROJECT.git"
          },
          "scripts": {
            "test": "./node_modules/.bin/karma start --single-run --browsers PhantomJS"
          },
          "devDependencies": {
            "karma-chrome-launcher": "~0.1.0",
            "karma-firefox-launcher": "~0.1.0",
            "karma-script-launcher": "~0.1.0",
            "karma-html2js-preprocessor": "~0.1.0",
            "karma-jasmine": "~0.1.3",
            "karma-requirejs": "~0.1.0",
            "karma-coffee-preprocessor": "~0.1.0",
            "karma-phantomjs-launcher": "~0.1.0",
            "karma": "~0.10.4",
            "karma-coverage": "~0.1.0",
            "grunt": "~0.4.1",
            "grunt-karma": "~0.6.2",
            "zlib": "*",
            "uglify-js": "*",
            "grunt-contrib-uglify": "~0.2.1",
            "grunt-contrib-jshint": "~0.5.4",
            "grunt-contrib-compress": "~0.5.0",
            "grunt-contrib-copy": "~0.4.1",
            "grunt-contrib-concat": "~0.3.0",
            "karma-junit-reporter": "~0.1.0"
          },
          "github": "https://github.com/USER/PROJECT"
        }

* Create a karma.conf.js in root.

        module.exports = function(config) {
          config.set({
            // base path, that will be used to resolve files and exclude
            basePath: '',

            frameworks: ['jasmine'],

            // list of files / patterns to load in the browser
            files: [
              'src/*.js',
              'test/*.js'
            ],

            // list of files to exclude
            exclude: [],
            preprocessors: {
              'src/*.js': ['coverage']
            },
            // use dots reporter, as travis terminal does not support escaping sequences
            // possible values: 'dots', 'progress'
            // CLI --reporters progress
            reporters: ['progress', 'junit', 'coverage'],

            junitReporter: {
              // will be resolved to basePath (in the same way as files/exclude patterns)
              outputFile: 'test-results.xml'
            },

            // web server port
            // CLI --port 9876
            port: 9880,

            // enable / disable colors in the output (reporters and logs)
            // CLI --colors --no-colors
            colors: true,

            // level of logging
            // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
            // CLI --log-level debug
            logLevel: config.LOG_INFO,

            // enable / disable watching file and executing tests whenever any file changes
            // CLI --auto-watch --no-auto-watch
            autoWatch: true,

            // Start these browsers, currently available:
            // - Chrome
            // - ChromeCanary
            // - Firefox
            // - Opera
            // - Safari (only Mac)
            // - PhantomJS
            // - IE (only Windows)
            // CLI --browsers Chrome,Firefox,Safari
            browsers: ['PhantomJS'],

            // If browser does not capture in given timeout [ms], kill it
            // CLI --capture-timeout 5000
            captureTimeout: 20000,

            // Auto run tests on start (when browsers are captured) and exit
            // CLI --single-run --no-single-run
            singleRun: true,

            // report which specs are slower than 500ms
            // CLI --report-slower-than 500
            reportSlowerThan: 500,

            plugins: [
              'karma-jasmine',
              'karma-chrome-launcher',
              'karma-firefox-launcher',
              'karma-junit-reporter',
              'karma-coverage',
              'karma-phantomjs-launcher'
            ]
          });
        };

* Create a changelog.txt file in root

        X.X.X
            CHANGES_MADE_IN_VERSION

* Create a .jshintrc file in src

        {
          "boss": true,
          "curly": true,
          "eqeqeq": true,
          "eqnull": true,
          "expr": true,
          "immed": true,
          "noarg": true,
          "onevar": true,
          "quotmark": "single",
          "smarttabs": true,
          "trailing": true,
          "undef": true,
          "unused": true,

          "sub": true,

          "browser": true,
          "es5": false,

          "globals": {
            "GLOBAL_1": true,   // Put global variables
            "GLOBAL_2": true
          }
        }

* Create a Gruntfile.js file in root

        module.exports = function (grunt) {

          var readOptionalJSON = function (filepath) {
              var data = {};
              try {
                data = grunt.file.readJSON(filepath);
              } catch (e) {}
              return data;
            },
            srcHintOptions = readOptionalJSON('src/.jshintrc');
          // Project configuration.
          grunt.initConfig({
            pkg: grunt.file.readJSON('package.json'),
            jshint: {
              dist: {
                src: [ "src/MAIN_FILE.js" ],
                options: srcHintOptions
              }
            },
            karma: {
              unit: {
                configFile: 'karma.conf.js'
              }
            },
            concat: {
              options: {
                separator: ';'
              },
              dist: {
                src: ['OTHER_PATHS_TO_FILES_TO_BE_CONCATENATED', 'src/PROJECT_NAME.js'],
                dest: 'versions/PROJECT_NAME.js'
              }
            },
            uglify: {
              options: {
                banner: '/*! PROJECT_NAME.js v<%= pkg.version %> | Date:<%= grunt.template.today("yyyy-mm-dd") %> |' +
                  ' License: https://raw.github.com/USER/PROJECT_NAME/master/LICENSE|' +
                  ' (c) FULL_YEAR\n' +
                  '//@ sourceMappingURL=PROJECT_NAME.min.map\n' +
                  '*/\n',
                preserveComments: "some",
                sourceMap: 'versions/PROJECT_NAME.min.map',
                sourceMappingURL: "PROJECT_NAME.min.map",
                report: "min",
                beautify: {
                  ascii_only: true
                },
                compress: {
                  hoist_funs: false,
                  join_vars: false,
                  loops: false,
                  unused: false
                },
                mangle: {
                  // saves some bytes when gzipped
                  except: [ "undefined" ]
                }
              },
              build: {
                src: ['versions/PROJECT_NAME.js'],
                dest: 'versions/PROJECT_NAME.min.js'
              }
            },
            compress: {
              main: {
                options: {
                  mode: 'gzip'
                },
                expand: true,
                cwd: 'versions/',
                src: ['PROJECT_NAME.min.js'],
                dest: 'versions/'
              }
            }
          });

          // Load the plugins
          grunt.loadNpmTasks("grunt-contrib-jshint");
          grunt.loadNpmTasks('grunt-karma');
          grunt.loadNpmTasks('grunt-contrib-concat');
          grunt.loadNpmTasks('grunt-contrib-uglify');
          grunt.loadNpmTasks('grunt-contrib-compress');

          // Default task(s).
          grunt.registerTask('default', ['jshint', 'karma', 'concat', 'uglify', 'compress']);
        };

* Create a bower.json file in root

        {
          "name": "PROJECT_NAME",
          "version": "X.X.X",
          "repository": {
            "type": "git",
            "url": "git://github.com/USER/PROJECT.git"
          }
        }

* Create a .travis.yml file in root.

        language: node_js
        node_js:
            - "0.10"
            - "0.8"
            - "0.6"
        before_install:
          - wget http://phantomjs.googlecode.com/files/phantomjs-1.7.0-linux-i686.tar.bz2
          - tar -xf phantomjs-1.7.0-linux-i686.tar.bz2
          - sudo rm -rf /usr/local/phantomjs
          - sudo mv phantomjs-1.7.0-linux-i686 /usr/local/phantomjs

* Open the terminal
* Install grunt-cli globally

        npm install -g grunt-cli
* Change the directory to your project path.

        cd PATH_TO_MY_PROJECT_ROOT_DIRECTORY

* Install your project dependencies

        npm install

* Create your test file/s in test folder
* Create your source file/s in src folder.
* Use TDD to write your code.
    * Use Jasmine as test framework
    * Add a new testcase
    * Execute your tests

            grunt karma

    * Make pass the tests.
    * Execute your tests

            grunt karma

    * Refactor your source and test code.
    * Come back to the 'Add a new testcase' step and repeat until you finish your code.
* Launch the build to get:
    * Your code syntax checked
    * Your code tested
    * Your code coverage
    * A concatenated file version
    * A minified file version
    * A gzipped file version

        grunt

##Update your project

* Change version in package.json
* Add version and changes in changelog.txt
* Change version in bower.json
* Change version in README.md
* If you need to give more info to the user add or modify the README.md content
* Execute the build.

    grunt

* Commit and push your changes to the repository
    * Add the version and the changelog.txt
* If is a new release.
    * Open the terminal
    * Change the directory to your project path.

        cd PATH_TO_MY_PROJECT_ROOT_DIRECTORY

    * Create a tag

        git tag -a X.X.X -m 'X.X.X'

    * Share your tag to remote

        git push origin X.X.X

* If you have to update a version
    * Open the terminal
    * Change the directory to your project path.

        cd PATH_TO_MY_PROJECT_ROOT_DIRECTORY

    * Delete the tag

        git tag -d X.X.X

    * Delete the remote tag

        git push origin :ref/tags/X.X.X

    * Create a tag

        git tag -a X.X.X -m 'X.X.X'

    * Share your tag to remote

        git push origin X.X.X

* Check your tags
    * Open the terminal
    * Change the directory to your project path.

        cd PATH_TO_MY_PROJECT_ROOT_DIRECTORY

    * Check your tags

        git tag

    * See the list of tags

* Check your releases in Github

    * Open https://github.com/USER/PROJECT_NAME/releases