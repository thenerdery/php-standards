# The Nerdery PHP Standards

The Nerdery PHP Standards and Best Practices embraces [PSR-2] and adds some
additional standards to it.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

[PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[RFC 2119]: http://tools.ietf.org/html/rfc2119

# 1.0 File Formatting

## 1.1 Character Encoding

PHP code MUST use only UTF-8 character encoding without BOM.

## 1.2 PHP Tags

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.

The closing `?>` tag MUST be omitted from files containing only PHP.

## 1.3 Indentation

Code MUST use an indent of 4 spaces, and MUST NOT use tabs for indenting.

> N.b.: Using only spaces, and not mixing spaces with tabs, helps to avoid
> problems with diffs, patches, history, and annotations. The use of spaces
> also makes it easy to insert fine-grained sub-indentation for inter-line 
> alignment.

## 1.4 Lines

The soft limit on line length MUST be 120 characters; automated style checkers
MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD
be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

There MUST NOT be more than one statement per line.

All PHP files MUST use the Unix LF (linefeed) line ending.

## 1.5 Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

# 2.0 Namespaces

## 2.1 PSR-0 Compliance

A fully-qualified namespace and class must have the following structure:
`\<Vendor Name>\(<Namespace>\)*<Class Name>`

Each namespace must have a top-level namespace ("Vendor Name").

Each namespace can have as many sub-namespaces as desired.

Each namespace separator is converted to a `DIRECTORY_SEPARATOR` when loading
from the file system.

Each `_` character in the CLASS NAME is converted to a `DIRECTORY_SEPARATOR`.
The `_` character has no special meaning in the namespace.

The fully-qualified namespace and class is suffixed with `.php` when loading
from the file system.

Alphabetic characters in vendor names, namespaces, and class names may be of
any combination of lower case and upper case.

## 2.2 Namespace Naming Convention

The "Vendor Name" should typically refer to the client name.

## 2.3 Namespace and Use Declarations

When present, there MUST be one blank line after the `namespace` declaration.

When present, all `use` declarations MUST go after the `namespace`
declaration.

There MUST be one `use` keyword per declaration.

There MUST be one blank line after the `use` block.

## 2.4 Formal Namespaces

Code written for PHP 5.3 and after MUST use formal namespaces.

All code must be written in PHP 5.3 and above.

## 2.5 Legacy Support

For backwards compatibility and support of legacy code only, code written for
5.2.x and before SHOULD use the pseudo-namespacing convention of `Vendor_`
prefixes on class names.

# 3.0 Keywords and Constants

## 3.1 Keywords

PHP [keywords] MUST be in lower case.

## 3.2 PHP Constants

The PHP constants `true`, `false`, and `null` MUST be in lower case.

## 3.3 Defined Constants

All letters used in a constant name must be capitalized, while all words in a
constant name must be separated by underscore characters.

For example, `EMBED_SUPPRESS_EMBED_EXCEPTION` is permitted but
`EMBED_SUPPRESSEMBEDEXCEPTION` is not.

[keywords]: http://php.net/manual/en/reserved.keywords.php

# 4.0 Classes

The term "class" refers to all classes, interfaces, and traits.

## 4.1 One Class Per File

In accordance with PSR-0, only one class should be defined in a single PHP file.

## 4.2 Class Names

Class names MUST be declared in `StudlyCaps`.

## 4.3 Class Declaration

The opening brace for the class MUST go on its own line; the closing brace
for the class MUST go on the next line after the body.

The `extends` and `implements` keywords MUST be declared on the same line as
the class name.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Lists of `implements` MAY be split across multiple lines, where each
subsequent line is indented once. When doing so, the first item in the list
MUST be on the next line, and there MUST be only one interface per line.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

## 4.4 Class Body

All code in a class must be indented by one level of indentation.

## 4.5 Class Constants

Class constants MUST be declared in all upper case with underscore separators.
For example:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```
# 5.0 Properties

## 5.1 Property Names

Property names MUST start with a lowercase letter and follow the `camelCase`
naming convention. 

Property names SHOULD only contain alphanumeric characters. Underscores are not
permitted.

Property names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

## 5.2 Property Declaration

Any properties declared in a class must be listed at the top of the class,
above the declaration of any methods.

Visibility MUST be declared on all properties.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

A property declaration looks like the following.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

# 6.0 Methods

## 6.1 Method Names

Method names MUST be declared in `camelCase()`.

Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

## 6.2 Method Declaration

Visibility MUST be declared on all methods.

Method names MUST NOT be declared with a space after the method name. The
opening brace MUST go on its own line, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```    

## 6.3 Method Signature Modifiers

When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

When present, the `static` declaration MUST come after the visibility
declaration.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

## 6.4 Method Arguments

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument
list.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

Pass-by-reference is the only parameter passing mechanism permitted in a method
declaration. Call-time pass-by-reference is strictly prohibited.

Note: As of PHP 5.3.0, you will get a warning saying that "call-time
pass-by-reference" is deprecated when you use `&` in `foo(&$a);`. And as of PHP
5.4.0, call-time pass-by-reference was removed, so using it will raise a fatal
error.

## 6.5 Global Functions

Functions in the global scope (a.k.a "floating functions") are permitted but
discouraged in most cases. Consider wrapping these functions in a static class.

## 6.6 Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

# 7.0 Variables

Variable names MUST start with a lowercase letter and follow the `camelCase`
naming convention. 

Variable names SHOULD only contain alphanumeric characters. Underscores are not
permitted.

# 8.0 Strings

## 8.1 Usage of Quotes

For defining string values, there is no standard on whether to use single
quotes or double quotes. String definitions should be consistent and
meaningful.

## 8.2 Variable Substitution

Variable substitution within strings is permitted using either of these forms:

```php
$greeting = "Hello $name, welcome back!";
$greeting = "Hello {$name}, welcome back!";
```

For consistency, this form is not permitted:

```php
$greeting = "Hello ${name}, welcome back!";
```

## 8.3 String Concatenation

When strings are concatenated using the `.` operator, a space must always be
added before and after the `.` operator to improve readability.

```php
$company = $firstName . ' ' . $lastName;
```

When concatenating strings spanning multiple lines with the "." operator, it is
encouraged to break the statement into multiple lines to improve readability.
In these cases, each successive line should be padded with white space such
that the "." operator is indented one level or aligned under the "=" operator.

```php
$url = 'http://'
    . $someClassNameThatIsLong->domain . '/'
    . $router->getUrl(array('action' => 'foobar'));

$anotherUrl = 'http://'
    . $someClassNameThatIsLong->domain . '/'
    . $router->getUrl(array('action' => 'bazquux'));
```

# 9.0 Arrays

## 9.1 Array Definition

When defining arrays with the `array()` language construct or the
short array syntax, there MUST be one space after each comma.

```php
$sampleArray = array(1, 2, 3, 'Zend', 'Studio');
$sampleArray = [1, 2, 3, 'Zend', 'Studio'];

$sampleArray = array('foo' => 'bar', 'baz' => 'quux');
$sampleArray = ['foo' => 'bar', 'baz' => 'quux'];
```

## 9.2 Multi-line Array Definition

When array definition spans multiple lines, the following rules should be
observed:

 - The first item MUST begin on the line following the array declaration.
 - Array items SHOULD be indented one level greater than the line containing
   the array declaration.
 - The closing parenthesis or square bracket MUST be on a line by itself and at
   the same
   indendation level as the line containing the array declaration.
 - A trailing comma SHOULD be present following the last item in the array.

```php
$sampleArray = array(
    "lorem ipsum",
    "cheezeburgers",
    "there's trouble at the mill",
);

$sampleArray = array(
    'firstKey' => 'firstValue',
    'secondKey' => 'secondValue',
);

$sampleArray = [
    'firstKey' => 'firstValue',
    'secondKey' => 'secondValue',
];
```

It is not required to line up the double arrows for associative arrays.

# 10.0 Control Structures

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening
  brace
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, and reduces the likelihood of introducing errors as new
lines get added to the body.


## 10.1 `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `elseif` are on the same line as the
closing brace from the earlier body.

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.

Within the conditional statements between the parentheses, operators must be
separated by spaces for readability.

```php
if ($a != 2 && $b != 3) {
    // some code
}
```

If a conditional statement must be broken into multiple lines, break the line
prior to a logic operator and indent the line one indentation level. The
closing parenthesis should be placed on a line with the closing brace of the
statement with a space between. The final line should be at a indentation level
equivalent to the opening control statement (the `if`).

```php
if (($a == $b)
    && ($b == $c)
    || (Foo::CONST == $d)
) {
    $a = $d;
}
```

## 10.2 `switch`, `case`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. The `case` statement MUST be indented once
from `switch`, and the `break` keyword (or other terminating keyword) MUST be
indented at the same level as the `case` body. There MUST be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

## 10.3 `while`, `do while`

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
while ($expr) {
    // structure body
}
```

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php
do {
    // structure body;
} while ($expr);
```

## 10.4 `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

## 10.5 `foreach`
    
A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

## 10.6 `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

## 10.7 `return`, `require`, `include`

The language constructs `return`, `require`, `include`, `require_once` and
`include_once` should not include parenthesis when invoked;

```
$autoloader = require_once 'vendor/autoload.php';

return $autoloader;
```

## 10.8 Ternary Operator

The ternary operator syntax (`?:`) should be used sparingly and only with
simple expressions that don't make the line too long or hard to read.

```php
$postCount = $parent->hasPosts() ? $parent->getPostId() : 0;
```

If a line with a ternary operation needs to span multiple lines, the statement
should be broken up into three lines where each line begins with the `?` and
`:` symbols respectively.

```php
$documentProcessingIndicatorId = $object->isProcessingDocument()
    ? $object->getDocumentProcessingIndicatorId()
    : null;
```

Avoid nesting of ternary operations as it hurts readability.

# 11.0 Closures

Closures MUST be declared with a space after the `function` keyword, and a
space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether or arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```

# 12.0 Documentation Blocks

All documentation blocks (docBlocks) must be compatible with the
*phpDocumentor* format. For more information, visit [phpdoc.org].

[phpdoc.org]: http://phpdoc.org

In general, each doc comment consists of a short description, an optional long
description and "tags". There must be one blank line between the short
description and the long description (if it exists), and one blank line
preceding the tags. Tags begin with an @-sign and provide specific
meta-data for the object being documented. Common tags include
`@package`, `@subpackage`, `@author` and `@version`.

Please see [phpdoc's tag reference] for a list of all the supported tags.

[phpdoc's tag reference]: http://phpdoc.org/docs/latest/references/phpdoc/tags/index.html

Package names (`@package`) should begin with a capital letter and
contain no spaces.

Don't use the `@category` tag as it is deprecated.

## 12.1 File Comments

Each file MAY contain a "file-level" doc comment at the top of the file.
This doc comment will define the purpose of the file and designate the package.

The following elements are required for file comments:

- `@package` -- The name of the package (project/client name or library name)

```php
<?php
/**
 * @package ProjectName
 */
```

## 12.2 Class Comments

Class files MAY contain a "class-level" doc comment immediately above the
class.

When including a "class-level" doc comment the following elements are required:
- Short Description
- `@package` -- The name of the package (project name or library name)

It is not recommended to include an `@author` tag or a `@version` tag in the
class level doc comment. These aspects of the codebase should be handled by the
version control system.

```php
/**
 * Short description for class
 *
 * Long description for class (if any)...
 */
```

## 12.3 Method and Function Comments

Function and Method declarations MUST include a doc comment immediately
preceding the declaration.

The following elements are required for function and method doc comments:

- `@param` -- Parameter tag for each argument in the function definition (only
  if there are arguments)
- `@return` -- The return value of the function. Use "void" if there is no
  return value

Parameter tags must appear immediately after the short or long description.

The format for `@param` tags is `@param <type> <variable name>
<comment>`.

It is not necessary to use the `@access` tag because the access level is
already known from the `public`, `private`, or `protected` modifier used to
declare the function.

If a function or method may throw an exception, use `@throws` for all
known exception classes:

```php
@throws exceptionclass [comment]
```

Note: There MUST be exactly one blank line before the tags in function
comments. There SHOULD NOT be a parameter description when the parameter name
is self-documenting. When a parameter requires a description, the description
SHOULD be provided in the method description.

```php
/**
 * Fetch user by id and organization
 *
 * @param int $userId
 * @param Organization $organization
 * @returns User|null
 */
public function fetchUserForOrganization($userId, Organization $organization)
{
    // ...
}
```

## 12.4 Property Comments

Every class property MUST have a doc comment that contains at a minimum:

- `@var` -- Tag indicating the data type

Class properties SHOULD have a doc comment that contains a description when the
property is not self-documenting.

```php
/**
 * Description
 *
 * @var string
 */
private $name = '';
```

Note: There must be exactly one blank line before the tags in property
comments.

## 12.5 Example

```php
<?php
/**
 * @package PackageName
 */

namespace VendorName\PackageName\ComponentOne;

/**
 * Short description for class
 *
 * Long description for class (if any)...
 */
class SampleClass
{
    /** 
     * Stores the options to use
     *
     * @var array
     */
    protected $options = array();

    /**
     * Constructor
     *
     * @param array $options Options to use
     * @return void
     */
    public function __construct($options = array())
    {
        // Some code ...
    }
}
```

# 13.0 Best Practices

## 13.1 Function and Variable Naming

When naming functions and variables, verbosity is generally encouraged.
Variables should always be as verbose as practical to describe the data that
the developer intends to store in them.  Terse variable names such as `$i` and
`$n` are discouraged for all but the smallest loop contexts. If a loop contains
more than 20 lines of code, the index variables should have more descriptive
names.

Plain variable names are discouraged. Here are examples of variable names that
you should avoid:

```
$var
$variable
$my*
$temp
$tmp
$foo
$baz
$quux
```

You are encouraged to prefix accessor methods for instance or static properties
with `get` or `set`, e.g. `getFirstName()` and `setFirstName` used to set the
property `$firstName` of an entity object.

## 13.2 Align Double-Arrows of Associative Arrays

You may choose to get into a pattern of aligning the `=>` double-arrow
assignment operator in array definitions. This can improve readability, but it
can also make diffs with version control noisy when new items are added to the
array that change the spacing.

```php
$sampleArray = array(
    'firstKey'  => 'first value',
    'secondKey' => 'second value',
    'short'     => 'short value',
);

$sampleArray = array(
    'firstKey'                => 'first value',
    'secondKey'               => 'second value',
    'short'                   => 'short value',
    'aLongKeyValueThatIsLong' => 'some value',
);
```

## 13.3 Public Properties Discouraged

Giving access to class properties directly by declaring them as public is
permitted but discouraged in favor of accessor methods (set & get).

## 13.4 Avoid Committing Commented Out Code

It is recommended that any block of code that is commented out should be
removed.

## 13.5 Avoid Large Classes

Any class that is greater than 750 lines should be considered for revising to
separate logic.

## 13.6 Avoid Database Queries in Controller Logic

Database query strings are prohibited from being used within MVC controllers.
Instead, they should be moved to the Model layer for proper separation of
duties. For instance, the following code should never be used in a controller:

```php
$sql = "SELECT * FROM users";
```

## 13.7 Remove Debug Code

Debug code, including the PHP functions `print_r()` and `var_dump()` must not
be used except while debugging. Do not commit debug code.
