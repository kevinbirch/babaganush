# babaganush

Babaganush is a wrapper for these static analysis tools:

* [PyFlakes](https://launchpad.net/pyflakes)
* [PEP8](https://github.com/jcrocholl/pep8)
* [Flake8](http://github.com/bmcustodio/flake8)

It supports all of the great features of these tools as pass-throughs and adds:

* It can run a single tool (i.e. run only PyFlakes or PEP8)
* Consistent, configurable output format for all tools
* Any code reported by a tool can be classified as error, warning or info 

## Usage

```shell
$ pycheck <path>
```

You can invoke this tool against any single python file or a directory to be scanned recursively for python files (*.py) to evaluate.

The output of all tools run will be merged and formatted and classified according to the settings.  The default tool to run is Flake8, and the native settings files for both the PEP8 and Flake8 tools are supported.  Any Flake8 plugins will be run according to Flake8 settings.

## Configuration

The following options are supported from both the command line and the config file:

* ignore - a comma separated list of codes to ignore
* checkers - a comma separted list of checkers to run
* format - the output format to use to report 
* info - a comma separated list of codes to consider informational
* warnings - a comma separated list of codes to consider warnings
* errors - a comma separated list of codes to consider errors

N.B. - If no codes are specified to be ignored, both PEP8 and Flake8 ignore E226, E241 and E242 by default.

## Output Formatting

The format that is used to report tool output can be set with the `format` configuration.  The default value is:

```
{filename}:{line}:{level} {code} {message}.\n
```

It uses the standard Python [string format](http://docs.python.org/2/library/string.html#format-string-syntax) syntax, so it's easy to organize by keyword.

## Issue Classification

The issues reported by the tools can be classified as errors, warnings or informational.  This can be used in conjunction with your editor to better visually classify the reported issue, or with version control hooks.

The configuration options `info`, `warnings` and `errors` will classify reported issues accordingly and the associated level will be reported in the `{code}` format keyword.

By default, the following codes are warnings (all others default to errors):

* W191 - indentation contains tabs
* W291 - trailing whitespace
* W292 - no newline at end of file
* W293 - blank line contains whitespace
* W391 - blank line at end of file
* W601 - `.has_key()` is deprecated, use `in`
* W602 - deprecated form of raising exception
* W603 - `<>` is deprecated, use `!=`
* W604 - backticks are deprecated, use `repr()`
* F401 - `module` imported but unused
* F811 - redefinition of unused `name` from line `N`

The error codes that were [introduced by Flake8 for PyFlakes](http://flake8.readthedocs.org/en/latest/warnings.html) are honored and used when PyFlakes is run by itself or through Flake8.

N.B. - any issue code reported by any tool or plugin of a tool can be classified in this way.

