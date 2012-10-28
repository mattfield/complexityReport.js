# complexityReport.js

A tool for reporting code complexity metrics in JavaScript projects
(still in development).

The metrics are calculated by walking syntax trees
generated by the [Esprima] parser.

[![Build status][ci-image]][ci-status]

## Installation

### Local to the current project

```
npm install complexity-report
```

### Globally for all projects

```
sudo npm install -g complexity-report
```

## Usage

### From the command line

```
cr [options] <file...>
```

#### Options

* `-o <file>`: Specify an output file for the report.
* `-f <format`: Specify an output format for the report.
* `-t <threshold>`: Specify the per-function complexity threshold
  (beyond which, will cause the process to fail when exiting).
* `-l`: Disregads operator `||` as a source of cyclomatic complexity.
* `-s`: Disegards `switch` statements as a source of cyclomatic complexity.
* `-i`: Treats `for`...`in` loops as a source of cyclomatic complexity.
* `-c`: Treats `catch` clauses as a source of cyclomatic complexity.

#### Output formats

These are loaded with `require` from the `src/formats` subdirectory.
Adding new formats is easy,
each module must export a function `format`
that takes a report object as its only argument
and returns a string representation of the report.
See `src/formats/plain.js` for an example format.

### From code

#### Loading the library

```
var cr = require('complexity-report');
```

#### Calling the library

```
var report = cr.run(source, options);
```

The argument `source` must be a string
containing the source code that is to be analysed.
The argument `options` is an optional object
which may contain properties that modify
cyclomatic complexity calculation.
The following options are available:

* `logicalor`: Boolean indicating whether operator `||`
  should be considered a source of cyclomatic complexity,
  defaults to `true`.
* `switchcase`: Boolean indicating whether `switch` statements 
  should be considered a source of cyclomatic complexity,
  defaults to `true`.
* `forin`: Boolean indicating whether `for`...`in` loops
  should be considered a source of cyclomatic complexity,
  defaults to `false`.
* `trycatch`: Boolean indicating whether `catch` clauses
  should be considered a source of cyclomatic complexity,
  defaults to `false`.

The returned report is an object
that contains properties detailing the complexity
of each function from the source code.
There is also an aggregate complexity score
for the source in its entirety.

## Development

### Roadmap

The current plan is
to add Halstead complexity measures
and the Maintainability Index,
then just focus on improving the calculations
by throwing more and more test cases together.
If you think there's anything else I should look at,
please raise an issue or,
even better, implement it and submit a pull request! :)

### Dependencies

The build environment relies on
[Node.js][node],
[NPM],
[Jake],
[JSHint],
[Mocha] and
[Chai].
Assuming that you already have Node.js and NPM set up,
you just need to run `npm install`
to install all of the dependencies
as listed in `package.json`.

### Unit tests

The unit tests are in `test/complexityReport.js`. You can run them with the
command `npm test` or `jake test`.

[ci-image]: https://secure.travis-ci.org/philbooth/complexityReport.js.png?branch=master
[ci-status]: http://travis-ci.org/#!/philbooth/complexityReport.js
[esprima]: http://esprima.org/
[node]: http://nodejs.org/
[npm]: https://npmjs.org/
[jake]: https://github.com/mde/jake
[jshint]: https://github.com/jshint/node-jshint
[mocha]: http://visionmedia.github.com/mocha
[chai]: http://chaijs.com/

