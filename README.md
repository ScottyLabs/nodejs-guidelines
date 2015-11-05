# nodejs-guidelines
A set of guidelines and linting configurations for ScottyLabs Node.js projects.

ScottyLabs Javascript code for core Tech projects uses [ES6][es6], the latest
stable revision of the EcmaScript standard.  For the forseeable future, this
means that all code that goes to the front-end must be transpiled with `babel`.

## Running the Linters
- Install the linters using `npm`:
```console
$ sudo npm install -g jscs jshint;
```

- Run them individually.  I'd recommend getting `jshint` to run clean first (it
  checks potential errors such as multiple variable definition), then get `jscs`
  to run clean (it primarily checks style).

```console
$ jshint -c ../path/to/jshintrc file.js;
$ jscs -c ../path/to/jscsrc file.js;
```

## Style

While style is primarily a matter of taste, non-emergency pull requests will not
accepted unless they match some basic guidelines.  First, they must run clean
with the JSCS and JSHint linters, using the configuration files in this
repository.  Of course, there are exceptions where conforming to a linter rule
would make the code much longer or verbose.  Remember, the reason we lint is to
help us make the code more readable, not to force us to conform to an arbitrary
ruleset that will inevitably have exceptions!  However, make sure there's a good
reason for ignoring a linter exception, and be prepared to explain your logic to
Tech Director/DevOps!

Furthermore, all files should contain a header comment that looks like so:
```js
/* @file <filename>.js
 * @brief A short, one to two line description of what this module does.
 * 
 * If a longer description is needed (and that's fine!) leave a space between us
 * and the previous line.  Don't worry about indenting inside this code block.
 *
 * @author Full Name (email@scottylabs)
 */
```

Each major function should be declared as so:
```js
// Great!
var x = function(args) { ... }
```
instead of 
```js
// Nope!
function x(args) { ... }
```
This is primarily for consistency in the code base.  It also makes it easier to
refactor this code and reason about its scope (since the latter is just
syntactical sugar for the former).

Every major function should also be documented by a block comment of this form:
```js
/* @brief Short description
 * 
 * [Optional] Long description

 * @param p1 Boolean Description
 * @param p2 Object Description
 * @param callback Function Description
 * @return Return value
 */
 var f = function(p1, p2, callback) { ... };
```

Globals should be decorated with `@brief` tags as well, if it's not super
obvious.  Those can start and end on the same line since they'll typically be
short.
```js
/* @brief The port the server listens on. */
var port = 8080;
```

Comments in a function should use the `//` syntax.

While this is covered by the linters (or should be), we typically use two space
indents, with no tabs in the file ANYWHERE.  Set up your editor to use this
notation!

Most other style issues should be hopefully covered by the linters (I've tried
to make them cover as much as possible).  These guidelines will likely grow as I
find things I don't want in the code base that aren't covered by a linter.
