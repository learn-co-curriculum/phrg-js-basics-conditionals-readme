# JavaScript Conditionals

## Objectives
1. Explain what constitutes an expression in JavaScript.
2. Organize code using block statements.
3. Describe the difference between truthy and falsy values.
4. Employ `if...else` statements to conditionally execute blocks of code.
5. Use a `switch` statement to selectively execute code based on the value of
an expression.
6. Rewrite an `if...else` as a one-liner with the ternary operator.

## Overview
In all facets of life, we constantly make conditional choices:
- `if` hungry :arrow_right: make sandwich.
  + `else` :arrow_right: don't make sandwich.
- `if` light is green :arrow_right: press gas pedal.
  + `else` :arrow_right: press brake pedal.
- `if` it's the first of the month :arrow_right: pay rent.
  + `else` :arrow_right: don't pay rent.

Writing code involves the same type of logic — we only want an action to happen
_if_ a certain condition is met. In the programming world, this is called
**control flow** because, well, it helps _control_ the _flow_ of an application.

Before we dive into JavaScript's conditional structures, let's go over a few
concepts that provide the syntactic underpinnings.

## Expressions
A JavaScript expression is **a unit of code that returns a value**. Primitive
values are expressions because they resolve to a value:

```js
9
// => 9

'Hello, world!'
// => "Hello, world!"

false
// => false
```

So are arithmetic and string operations. This code resolves to the number `64`:

```js
8 * 8
// => 64
```

And this resolves to the string `"Hello, world!"`:

```js
'Hello, ' + 'world!'
// => "Hello, world!"
```

Ditto for comparison and assignment operations. This comparison resolves to the
boolean `true`:

```js
2 > 1
// => true
```

Variable declarations are NOT expressions...

```js
let answer;
```

...but variable assignments ARE, resolving to the assigned value (`42`, in this
  case):

```js
answer = 42;
// => 42
```

Finally, references to variables are also expressions, resolving to the value
contained in the variable:

```js
const fullName = 'Ada Lovelace';

fullName;
// => "Ada Lovelace"
```

## Block statements

A block statement is a pair of curly braces (`{ }`) used to group JavaScript
statements. It plays a featured role in conditional statements, loops, and
functions.

```js
{
  'This line is a JavaScript statement nested inside a block statement!';

  // This is also a statement nested inside a block:
  5 * 5 - 5

  // And so are these:
  const weCan = 'group multiple statements';

  const suchAs = 'these variable declarations';

  const insideA = 'block statement.';
}
// => 20
```

Block statements return the value of the last evaluated expression inside the
curly braces. In the above example, the variable declarations are _not_
expressions, so the value of `5 * 5 - 5` is returned.  

**Note**: The statement above _implicitly_ returns 20 (the value returned by
`5 * 5 - 5`, when evaluated). Functions, which we will discuss
in an upcoming lesson, also contain all of their code inside curly braces, but
for functions, we need to _explicitly_ use the word `return` to tell
JavaScript what we want the output to be (if we want one, at all).  Just
remember that the _implicit return is something unique to block statements_ like
the ones we use for `if...else` and loop statements.

## Truthiness and falsiness
Truthiness and falsiness indicate what happens when the value is converted into
a boolean. If, upon conversion, the value becomes `true`, we say that it's a
**truthy** value. If it becomes `false`, we say that it's **falsy**.

In JavaScript, the following values are **falsy**:
- `false`
- `null`
- `undefined`
- `0`
- `NaN`
- An empty string (` `` `, `''`, `""`)

***Every other value is truthy***.

To check whether a value is truthy or falsy in our browser's JS console, we can
pass it to the global `Boolean` object, which converts the value into its
boolean equivalent:

```js
Boolean(false);
// => false

Boolean(null);
// => false

Boolean(undefined);
// => false

Boolean(0);
// => false

Boolean(NaN);
// => false

Boolean('');
// => false

Boolean(true);
// => true

Boolean(42);
// => true

Boolean('Hello, world!');
// => true

Boolean( { firstName: 'Brendan', lastName: 'Eich' } );
// => true
```

***NOTE***: `document.all` is also falsy, but don't worry about it for now. (Or
  ever, really — it's an imperfect solution for legacy code compatibility.)

Ready to put that killer new vocabulary to the test? Here we go!

## Conditional statements
In JavaScript, we use three structures for implementing condition-based control
flow: the `if...else` statement, `switch` statement, and ternary operator.

### `if` statement
`if` statements are the most common type of conditional, and they're pretty
straightforward:

```js
if (condition) {
  // Block of code
}
```

If the condition returns a **truthy** value, run the code inside the **block**:

```js
const age = 30;

let isAdult;

if (age >= 18) {
  isAdult = true;
}
// => true

isAdult;
// => true
```

If the condition returns a **falsy** value, do nothing:

```js
const age = 14;

let isAdult;

if (age >= 18) {
  isAdult = true;
}

isAdult;
// => undefined
```

#### `else`
If we want to run some code when the condition returns a `falsy` value, we can
use an `else` clause:

```js
const age = 14;

let isAdult;

if (age >= 18) {
  isAdult = true;
} else {
  isAdult = false;
}
// => false

isAdult;
// => false
```

#### Nested conditionals
If we have multiple overlapping conditions, we can employ nested conditional
statements. For example, instead of just deciding whether the passed-in `age`
meets the criteria for `isAdult`, let's add in some other hallmarks of
burgeoning adulthood (in American society, at least): `canVote`, `canEnlist`,
and `canDrink`. 16-year-olds can vote; 18-year-olds can vote, enlist, and are
legal adults; and 21-year-olds can vote, enlist, are legal adults, and can
drink. Let's nest those bad boys up:

```js
const age = 17;

let isAdult, canVote, canEnlist, canDrink;

if (age >= 16) {
  canVote = true;

  if (age >= 18) {
    isAdult = true;
    canEnlist = true;

    if (age >= 21) {
      canDrink = true;
    }
  }
}

isAdult;
// => undefined

canVote;
// => true

canEnlist;
// => undefined

canDrink;
// => undefined
```

#### `else if`
Another way to represent multiple possible conditions is with `else if` clauses:

```js
const age = 20;

let isAdult, canVote, canEnlist, canDrink;

if (age >= 21) {
  isAdult = true;
  canVote = true;
  canEnlist = true;
  canDrink = true;
} else if (age >= 18) {
  isAdult = true;
  canVote = true;
  canEnlist = true;
} else if (age >= 16) {
  canVote = true;
}
// => true

isAdult;
// => true

canVote;
// => true

canEnlist;
// => true

canDrink;
// => undefined
```

As soon as one of the conditions returns a truthy value, the attached code
block runs and the conditional exits. If none of the conditions evaluate to a
truthy value, then the `else` code block runs (or, in the absence of an `else`
clause, the conditional simply exits). Note that, unlike the nested `if`
statements above, **at most one code block will run**. In the absence of an
`else` statement, it's possible that none of the `if` conditions return a
truthy value and **no block is run**. However, it's impossible for more than
one block in a linked `if...else if...else` control flow to run.

## `switch`

Running multiple blocks in the same control flow is one of the many talents of
the `switch` statement. The general structure is as follows:

```js
switch (expression) {
  case value1:
    // Statements
    break;
  case value2:
    // Statements
    break;
  default:
    // Statements
    break;
}
```

The JavaScript engine evaluates the expression and then compares the returned
value against each of the `case` values _using strict equality_ (`===`):

```js
const hunger = 'famished';

let food;

switch (hunger) {
  case 'light':
    food = 'grapes';
    break;
  case 'moderate':
    food = 'sushi';
    break;
  case 'famished':
    food = 'lasagna';
    break;
}
// => "lasagna"

food;
// => "lasagna"
```

Generally, we use a `switch` statement if we need a conditional that hinges on
a single value but requires a separate handler for each potential case. For
example, the `switch` statement here doesn't require us to repeat the
`if (order === _____)` line for each possibility:

```js
const order = 'cheeseburger';

let ingredients;

switch (order) {
  case 'cheeseburger':
    ingredients = 'bun, burger, cheese, lettuce, tomato, onion';
    break;
  case 'hamburger':
    ingredients = 'bun, burger, lettuce, tomato, onion';
    break;
  case 'malted':
    ingredients = 'milk, ice cream, malted milk powder';
    break;
  default:
    console.log("Sorry, that's not on the menu right now.");
    break;
}

if (order === 'cheeseburger') {
  ingredients = 'bun, burger, cheese, lettuce, tomato, onion';
} else if (order === 'hamburger') {
  ingredients = 'bun, burger, lettuce, tomato, onion';
} else if (order === 'malted') {
  ingredients = 'milk, ice cream, malted milk powder';
} else {
  console.log("Sorry, that's not on the menu right now.");
}
```

We can also assign the same set of statements to multiple cases. In the
following example, if the `age` variable contains any number between `13` and
`19`, the `isTeenager` variable will be set to `true`. If it contains anything
other than a number between `13` and `19`, none of our `case`s will hit, and it
will end up at the `default`, which sets `isTeenager` to `false`:
```js
const age = 15;

let isTeenager;

switch (age) {
  case 13:
  case 14:
  case 15:
  case 16:
  case 17:
  case 18:
  case 19:
    isTeenager = true;
    break;
  default:
    isTeenager = false;
    break;
}
```

The `default` and `break` keywords are both optional in basic `switch`
statements, but useful.  In more complicated statements, they become necessary
to ensure the correct flow

#### `break`
When the JavaScript engine reaches a `break`, it exits the entire `switch`
statement. By leaving a `break` at the end of each `case`'s set of statements,
we ensure that the `switch` statement will match at most a single `case`. Once
it matches the first `case`, it will run that `case`'s statements and then
exit. In addition to not accidentally matching multiple `case`s, this also
provides a small performance boost because the JavaScript engine doesn't always
have to check every single `case`.

However, sometimes we do want to potentially match multiple cases, and we will
need to leave out `break` in order to do this. There's a neat little trick we
can employ that allows us to use comparisons for `case` statements. Let's
rewrite the above `if...else` chain as a more compact, less repetitious
`switch` statement:

```js
const age = 20;

let isAdult, canVote, canEnlist, canDrink;

switch (true) {
  case age >= 21:
    canDrink = true;
  case age >= 18:
    isAdult = true;
    canEnlist = true;
  case age >= 16:
    canVote = true;
}
// => true

isAdult;
// => true

canVote;
// => true

canEnlist;
// => true

canDrink;
// => undefined
```

We specified `true` as the value to `switch` on. All of our `case`s are
comparisons, and if the comparison returns `true` its statement(s) will be run.
Because we forwent `break` statements, we allow the JavaScript engine to
continue cascading down the `case`s **even if it matches one or more**. With
`age` set to `20` in the above example, the first `case`, `age >= 21`, returns
`false` and so the assignment of `canDrink` never happens. The engine then
proceeds to the next `case`, `age >= 18`, which returns `true`, assigning the
value `true` to `isAdult` and `canEnlist`. Since it encounters no `break`
statement, the JavaScript engine then evaluates the final `case`, `age >= 16`,
which also returns `true`. It assigns `true` to `canVote`, reaches the end of
the `switch` statement, and exits.

#### `default`
The `default` keyword specifies a set of statements to run after all of the
`switch` statement's `case`s have been checked. The only time the `default`
statements do _not_ run is if the engine hits a `break` in one of the `case`
statements.

```js
const mood = 'quizzical';

let response;

switch (mood) {
  case 'happy':
    response = 'Heck yea; be happy!';
  case 'sad':
    response = "You're awesome; keep your head up!";
  default:
    response = "Sorry, I don't know how to respond to that mood.";
}
// => "Sorry, I don't know how to respond to that mood."

response;
// => "Sorry, I don't know how to respond to that mood."
```

It's typically safer to include `break` statements because it helps avoid bugs
like this:

```js
const mood = 'happy';

let response;

switch (mood) {
  case 'happy':
    response = 'Heck yea; be happy!';
  case 'sad':
    response = "You're awesome; keep your head up!";
  default:
    response = "Sorry, I don't know how to respond to that mood.";
}
// => "Sorry, I don't know how to respond to that mood."

response;
// => "Sorry, I don't know how to respond to that mood."
```

The `'happy'` case matches and assigns the string `'Heck yea; be happy!'` to
`response`. However, since we didn't `break` after that assignment, the
`default` case _also_ runs and reassigns `"Sorry, I don't know how to respond
to that mood."` to `response`. Whoops!

### Ternary operator
The ternary operator, the final piece of the conditional puzzle, is a good way
to represent an `if...else` statement in a single line of code:

```js
condition ? expression1 : expression2;
```

If the condition returns a truthy value, run the code in `expression1`. If the
condition returns a falsy value, run the code in `expression2`.

```js
const age = 45;

let isAdult;

age >= 18 ? isAdult = true : isAdult = false;
// => true

isAdult;
// => true
```

In the above example, we assign `isAdult` as `true` if the condition returns a
truthy value and as `false` otherwise. We can simplify that a bit and assign
the result of the ternary directly to a variable:

```js
const age = 60;

const isAdult = age >= 18 ? true : false;

isAdult;
// => true
```

If it helps you visualize what's going on, you can wrap the condition, the
expressions, or the entire ternary in parentheses:
```js
const age = 17;

const isAdult = (age >= 18) ? true : false;

const canVote = age >= 16 ? (1 === 1) : (1 !== 1);

const canEnlist = (isAdult ? true : false);

isAdult;
// => false

canVote;
// => true

canEnlist
// => false
```

***Top Tip***: Be careful to not overuse the ternary operator. It's fine for
slimming down a simple `if...else`, but be conscious of how easy your code is
to understand for an outsider. Remember, you generally write code once, but it
gets read (by yourself and others) **far** more than once. The ternary is often
more difficult to quickly interpret than a regular old `if...else`, so make
sure the reduction in code is worth any potential reduction in readability.

## Flatbook examples
There are tons of control flow structures in the Flatbook code base.

### `if...else`
When a guest tries to log in, check whether the provided email and password
match an active account:

```js
let errorMessage = '';
let loggedIn = false;

// *User enters a valid email and password and clicks the Login button*
const email = 'avi@flatbook.com';
const password = 'j4v45cr1pt 15 4w350m3';

// *The Flatbook app then checks whether the provided email and password are valid*
const accountFound = true;
const passwordMatches = false;

if (email === '') {
  errorMessage = 'Please provide an email.';
} else if (password === '') {
  errorMessage = 'Please provide a password.';
} else {
  if (accountFound) {
    if (passwordMatches) {
      loggedIn = true;
    } else {
      errorMessage = "Sorry, that password doesn't match our records.";
    }
  } else {
    errorMessage = 'Sorry, no account matching the provided email address was found.';
  }
}
// => "Sorry, that password doesn't match our records."

loggedIn;
// => false

errorMessage;
// => "Sorry, that password doesn't match our records."
```

### Ternary operator
When a user logs in, check whether it's their birthday. If it is, set a
celebratory message to appear in a banner; _else_, set the message to an empty
string:

```js
const userBirthday = 'Dec 10';

const userFullName = 'Ada Lovelace';

let todaysDate = 'Dec 10';

const birthdayMessage = (todaysDate === userBirthday) ? `Happy birthday, ${userFullName}!` : '';

birthdayMessage;
// => "Happy birthday, Ada Lovelace!"
```

### `switch`
Once the user logs in, set their permissions based on the account type:

```js
const accountType = 'admin';

let permissionsLevel;
let canViewProfiles = false;
let canImpersonateUsers = false;

switch (accountType) {
  case 'guest':
    permissionsLevel = 0;
    break;
  case 'user':
    permissionsLevel = 10;
    canViewProfiles = true;
    break;
  case 'admin':
    permissionsLevel = 20;
    canViewProfiles = true;
    canImpersonateUsers = true;
    break;
}
// => true

permissionsLevel;
// => 20
```

It's easy to imagine hundreds of other conditionals that go into the
functioning of a large site like Flatbook. They're ubiquitous, so study up!

## Does this need an update?

Please open a [GitHub issue](https://github.com/learn-co-curriculum/phrg-js-basics-conditionals-readme/issues) or [pull-reqeust](https://github.com/learn-co-curriculum/phrg-js-basics-conditionals-readme/pulls). Provide a detailed description that explains the issue you have found or the change you are proposing. Then "@" mention your instructor on the issue or pull-reqeust, and send them a link via Connect.

## Resources
- MDN
  + [Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions)
  + [Block statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)
  + [Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) and [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)
  + [Conditional statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Conditional_statements)
    * [`if...else` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
    * [Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
    * [`switch` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
<p data-visibility='hidden'>PHRG JavaScript Conditionals</p>
