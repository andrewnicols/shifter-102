Example to demonstrate issue in https://github.com/yui/shifter/pull/102
=======================================================================

This example project includes three (empty) modules with a basic Shifter
configuration.

The Shifter configuration explicitly prevents coverage generation, however
Shifter takes the optional argument --coverage to override the setting
provided by configuration.

Respect of the default from config can be verified by:
```terminal
git checkout .
git clean -df
cd src/a
shifter
tree ../../build/a
```
(no coverage files should be found)

Equally, you can confirm that the --coverage option to Shifter does
override the config and force coverage generation:
```terminal
git checkout .
git clean -df
cd src/a
shifter --coverage
tree ../../build/a
```
(a-coverage.js shoudl be present)

You can also confirm that a shifter with --walk also respects the
configuration file:
```terminal
git checkout .
git clean -df
cd src
shifter --walk
tree ../../build
```
(no coverage files should be found)

However, walking Shifter with the option to force coverage is not
respected:
```terminal
git checkout .
git clean -df
cd src
shifter --walk --coverage
tree ../../build
```
In this case, coverage files should be present but are not.
