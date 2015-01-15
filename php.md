#PHP Style Guide
Modified from [PEAR coding standards](http://pear.php.net/manual/en/standards.php)

##Syntax

- Use soft tabs set to 2 spaces

##Control Structures

These include `if`, `for`, `while`, `switch`, etc. Here is an example if statement, since it is the most complicated of them:

```PHP
<?php
if (condition1 || condition2) {
  action1;
} elseif (condition3 && condition4) {
  action2;
} else {
  defaultaction;
}
?>
```

Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls.

You are strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added.
For switch statements:

```PHP
<?php
switch (condition) {
  case 1:
    action1;
    break;

  case 2:
    action2;
    break;

  default:
    defaultaction;
    break;
}
?>
```
##Function Definitions

No space between the function name and the parentheses. Put a space between arguments, and a space between the closing paraentheses and opening curly brace.

```PHP
<?php
function fooFunction($arg1, $arg2 = '') {
  if (condition) {
    statement;
  }
  return $val;
}
?>
```

##Function Calls

Functions should be called with no spaces between the function name, the opening parenthesis, and the first parameter.

Put spaces between commas and each parameter, and no space between the last parameter, the closing parenthesis, and the semicolon.

There should be one space on either side of an equals sign used to assign the return value of a function to a variable.

```PHP
<?php
$var = foo($bar, $baz, $quux);
?>
```

##Including Code

Anywhere you are unconditionally including a class file, use require_once. Anywhere you are conditionally including a class file (for example, factory methods), use include_once. Either of these will ensure that class files are included only once. They share the same file list, so you don't need to worry about mixing them - a file included with require_once will not be included again by include_once.

##Naming Conventions

- Class names should start with a captial and use underscores to separate words: `Log`, `Net_Finger`, `HTML_Upload_Error`.
- Variables and methods should use camelCase.
- Constants should always be all-uppercase, with underscores to separate words.

##Return early
To keep readability in functions and methods, it is wise to return early if simple conditions apply that can be checked at the beginning of a method. This can keep indentation and the brain power needed to follow the code low.

Instead of:

```PHP
<?php
function foo($bar, $baz) {
  if ($foo) {
    //assume
    //that
    //here
    //is
    //the
    //whole
    //logic
    //of
    //this
    //method
    return $calculated_value;
  } else {
    return null;
  }
}
?>
```

do this:

```PHP
<?php
function foo($bar, $baz) {
  if (!$foo) {
    return null;
  }

  //assume
  //that
  //here
  //is
  //the
  //whole
  //logic
  //of
  //this
  //method
  return $calculated_value;
}
?>
```
