# Node.js Style Guide

This is a guide for writing consistent and aesthetically pleasing node.js code.
It is inspired by what is popular within the community, and flavored with some
personal opinions.

This guide was originally created by [Felix Geisendörfer](http://felixge.de/) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license. You are encouraged to fork this repository and make adjustments
according to your preferences. This fork was first created to help with [mtwitter];
it is somewhat more strict, and contains a little more depth of detail for a number
of potentially contentious style points.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

[mtwitter]: https://github.com/passcod/mtwitter


### JSHint

Using the following options will help detecting a number of style points
in a semi-automated fashion.

```
node:     true    Code is running inside of the Node runtime environment
curly:    true    Always put curly braces around blocks in loops and conditionals
eqeqeq:   true    Prohibits the use of == and != in favor of === and !==
immed:    true    Prohibits the use of immediate function invocations without parens
indent:   2       Two spaces for indentation
latedef:  true    Prohibits the use of a variable before it was defined
noarg:    true    Prohibits the use of arguments.caller and arguments.callee
noempty:  true    Warns when you have an empty block in your code
nonew:    true    Prohibits the use of constructor functions for side-effects
plusplus: true    Prohibits the use of unary increment and decrement operators
quotmark: single  Enforces the consistency of quotation marks
undef:    true    Prohibits the use of explicitly undeclared variables
unused:   true    Warns when you define and never use your variables
trailing: true    Makes it an error to leave a trailing whitespace in your code
maxlen:   80      Line length

camelcase: true   Force all variable names to use either camelCase style or UPPER_CASE
newcap:    true   Requires you to capitalize names of constructor functions
nomen:     true   Disallows the use of dangling _ in variables
```


## 2 Spaces for indention

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

## No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

## Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
a core values of our community. Consider the points of [the opposition][], but
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

## Don't use ++ or --

Use `+= 1` or `-= 1` instead.

## 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

## Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
var foo = 'bar';
```

*Wrong:*

```js
var foo = "bar";
```

## Spacing around blocks

*Right:*

```js
if (iAmRight) {
  execute(this);
  execute(that);
}
```

*Wrong:*

```js
if (iAmWrong) {

  fooo();
}

function toBe(orNot) {
  baar();

}

try {

  baaz();

} catch { ... }
```


## Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

## Closing braces between related blocks

When using `else if`, `else`, or `catch`, put the closing brace of the
second block inline with the statement:

*Right:*

```js
if (true) {
  claim('Logic works!');
} else if (NaN === NaN) {
  despair();
} else {
  ohno('!');
}
```

*Wrong:*

```js
if (false) {
  shout('Down with you!');
}
else if ("" == 0) {
  hack();
}
else {
  calmly('disengage');
}
```


## Single-line conditionals

…are not allowed.

*Right:*

```js
if (true) {
  something();
}
```

*Wrong:*

```js
if (true) something();

if (true)
  something();

// Very wrong:
if (true)
something();
```


## Declare one variable per var statement

Declare one variable per var statement, it makes it easier to re-order the
lines. Ignore [Crockford][crockfordconvention] on this, and put those
declarations wherever they make sense. You can also align the `=` if it
makes things clearer.

*Right:*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (items.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (items.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

## Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
function BankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

## Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

Node.js / V8 actually supports mozilla's [const] extension, but
unfortunately that cannot be applied to class members, nor is it part of any
ECMA standard. _(Yes, [const is part of ES 6 / Harmony][constharmony], but that
is not stable in any way yet)_

*Right:*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const
[constharmony]: http://wiki.ecmascript.org/doku.php?id=harmony:const

## Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if (a === '') {
  console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators


## Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```

## Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptive variable:

*Right:*

```js
var isAuthorized = (user.isAdmin() || user.isModerator());
if (isAuthorized) {
  console.log('winning');
}
```

*Wrong:*

```js
if (user.isAdmin() || user.isModerator()) {
  console.log('losing');
}
```

## Functions with many arguments

```js
oauth = new oauth.OAuth(
  options.request_token_url,
  options.access_token_url,
  options.consumer_key,
  options.consumer_secret,
  '1.0',        // version
  null,         // authorize callback?
  'HMAC-SHA1',  // signature method
  null,         // nonce size
  this.options.headers
);

oauth.get(
  url,
  // ...
  content_type,
function(error, data, response) {
  handle();
});
```

- Closing _paren_ on newline, to demark a “block”
- All arguments on their own line
- Short comments to give precisions if necessary
- Callbacks start unindented, to group closing _paren_ and
  _bracket_; it also provides enough of a break to separate
  the “blocks”

### For smaller ones…

This is acceptable, especially to split long concatenation. Notice:

- The `+` is _before_ the split, just like a `,` would
- The second line is aligned with the quote, i.e. just _after_ the last
  opening brace
- This is short enough not to need the closing _parens_ aligned with
  the opening ones, as opposed to the example above

```js
callback(new Error('HTTP Error ' + response.statusCode + ': ' +
                   http.STATUS_CODES[response.statusCode]));
```

## Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

## Return early from functions

To avoid deep nesting of if-statements, always return a functions value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```


## Function() style

Crockford might damn your code, but the prevailing Node.js community style
doesn't use that space between `function` and the *parens*:

*Right:*

```js
function(arg) {
  // ...
}
```

*Wrong:*

```js
function (arg) {
  // ...
}
```


## Name your closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function() {
  console.log('losing');
});
```

## No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```

## Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.  
Use `/* ... */` for top-of-file headers only.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE'', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

## Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)


## EOF

All files should have a newline at the end (to make diffing cleaner).
