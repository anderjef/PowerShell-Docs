---
description: PowerShell providers allow access to data and components from the command line. The data is presented in a consistent format that resembles a file system drive.
ms.date: 05/19/2021
title: Basic concepts
---
# 3. Basic concepts

## Providers and drives

A *provider* allows access to data and components that would not otherwise be easily accessible at
the command line. The data is presented in a consistent format that resembles a file system drive.

The data that a provider exposes appears on a *drive*, and the data is accessed via a *path* just
like with a disk drive. Built-in cmdlets for each provider manage the data on the provider drive.

PowerShell includes the following set of built-in providers to access the different types of data
stores:

| **Provider** | **Drive Name**  | **Description**                     | **Ref.** |
|--------------|-----------------|-------------------------------------|----------|
| Alias        | Alias:          | PowerShell aliases                  | §3.1.1   |
| Environment  | Env:            | Environment variables               | §3.1.2   |
| FileSystem   | A:, B:, C:, ... | Disk drives, directories, and files | §3.1.3   |
| Function     | Function:       | PowerShell functions                | §3.1.4   |
| Variable     | Variable:       | PowerShell variables                | §3.1.5   |

Windows PowerShell:

| **Provider** |                    **Drive Name**                     |             **Description**              |
| ------------ | ----------------------------------------------------- | ---------------------------------------- |
| Certificate  | Cert:                                                 | x509 certificates for digital signatures |
| Registry     | HKLM: (HKEY_LOCAL_MACHINE), HKCU: (HKEY_CURRENT_USER) | Windows registry                         |
| WSMan        | WSMan:                                                | WS-Management configuration information  |

The following cmdlets deal with providers and drives:

- `Get-PSProvider`: Gets information about one or more providers (see §13.25)
- `Get-PSDrive`: Gets information about one or more drives (see §13.24)

The type of an object that represents a provider is described in §4.5.1. The type of an object that
represents a drive is described in §4.5.2.

### Aliases

An *alias* is an alternate name for a command. A command can have multiple aliases, and the original
name and all of its aliases can be used interchangeably. An alias can be reassigned. An alias is an
item (§3.3).

An alias can be assigned to another alias; however, the new alias is not an alias of the original
command.

The provider Alias is a flat namespace that contains only objects that represent the aliases. The
variables have no child items.

Some aliases are built in to PowerShell. (For those built-in cmdlets having aliases, those aliases
follow their cmdlets name in the section heading of §13.)

The following cmdlets deal with aliases:

- `New-Alias`: Creates an alias (see §13.33)
- `Set-Alias`: Creates or changes one or more aliases (see §13.46)
- `Get-Alias`: Gets information about one or more aliases (see §13.13)
- `Export-Alias`: Exports one or more aliases to a file (see §13.10)

When an alias is created for a command using `New-Alias`, parameters to that command cannot be
included in that alias. However, direct assignment to a variable in the Alias: namespace does permit
parameters to be included.

> [!NOTE]
> It is a simple matter, however, to create a function that does nothing more than contain the
> invocation of that command with all desired parameters, and to assign an alias to that function.

The type of an object that represents an alias is described in §4.5.4.

Alias objects are stored on the drive Alias: (§3.1).

### Environment variables

The PowerShell environment provider allows operating system environment variables to be retrieved,
added, changed, cleared, and deleted.

The provider Environment is a flat namespace that contains only objects that represent the
environment variables. The variables have no child items.

An environment variable's name cannot include the equal sign (`=`).

Changes to the environment variables affect the current session only.

An environment variable is an item (§3.3).

The type of an object that represents an environment variable is described in §4.5.6.

Environment variable objects are stored on the drive Env: (§3.1).

### File system

The PowerShell file system provider allows directories and files to be created, opened, changed, and
deleted.

The file system provider is a hierarchical namespace that contains objects that represent the
underlying file system.

Files are stored on drives with names like A:, B:, C:, and so on (§3.1). Directories and files are
accessed using path notation (§3.4).

A directory or file is an item (§3.3).

### Functions

The PowerShell function provider allows functions (§8.10) and filters (§8.10.1) to be retrieved,
added, changed, cleared, and deleted.

The provider Function is a flat namespace that contains only the function and filter objects.
Neither functions nor filters have child items.

Changes to the functions affect the current session only.

A function is an item (§3.3).

The type of an object that represents a function is described in §4.5.10. The type of an object that
represents a filter is described in §4.5.11.

Function objects are stored on drive Function: (§3.1).

### Variables

Variables can be defined and manipulated directly in the PowerShell language.

The provider Variable is a flat namespace that contains only objects that represent the variables.
The variables have no child items.

The following cmdlets also deal with variables:

- `New-Variable`: Creates a variable (see §13.37)
- `Set-Variable`: Creates or changes the characteristics of one or more variables (see §13.50)
- `Get-Variable`: Gets information about one or more variables (see §13.26)
- `Clear-Variable`: Deletes the value of one or more variables (see §13.5)
- `Remove-Variable`: Deletes one or more variables (see §13.42)

As a variable is an item (§3.3), it can be manipulated by most Item-related cmdlets.

The type of an object that represents a variable is described in §4.5.3.

Variable objects are stored on drive Variable: (§3.1).

## Working locations

The *current working location* is the default location to which commands point. This is the location
used if an explicit path (§3.4) is not supplied when a command is invoked. This location includes
the *current drive*.

A PowerShell host may have multiple drives, in which case, each drive has its own current location.

When a drive name is specified without a directory, the current location for that drive is implied.

The current working location can be saved on a stack, and then set to a new location. Later, that
saved location can be restored from that stack and made the current working location. There are two
kinds of location stacks: the *default working location stack*, and zero or more user-defined *named
working location stacks*. When a session begins, the default working location stack is also the
*current working location stack*. However, any named working location stack can be made the current
working location stack.

The following cmdlets deal with locations:

- `Set-Location`: Establishes the current working location (see §13.49)
- `Get-Location`: Determines the current working location for the specified drive(s), or the working
  locations for the specified stack(s) (see §13.21)
- `Push-Location`: Saves the current working location on the top of a specified stack of locations
  (see §13.39)
- `Pop-Location`: Restores the current working location from the top of a specified stack of
  locations (see §13.38)

The object types that represents a working location and a stack of working locations are described
in §4.5.5.

## Items

An *item* is an alias (§3.1.1), a variable (§3.1.5), a function (§3.1.4), an environment variable
(§3.1.2), or a file or directory in a file system (§3.1.3).

The following cmdlets deal with items:

- `New-Item`: Creates a new item (see §13.34)
- `Set-Item`: Changes the value of one or more items (see §13.48)
- `Get-Item`: Gets the items at the specified location (see §13.17)
- `Get-ChildItem`: Gets the items and child items at the specified location (see §13.14)
- `Copy-Item`: Copies one or more items from one location to another (see §13.9)
- `Move-Item`: Moves one or more items from one location to another (see §13.32)
- `Rename-Item`: Renames an item (see §13.43)
- `Invoke-Item`: Performs the default action on one or more items (see §13.29)
- `Clear-Item`: Deletes the contents of one or more items, but does not delete the items (see §13.4)
- `Remove-Item`: Deletes the specified items (see §13.40)

The following cmdlets deal with the content of items:

- `Get-Content`: Gets the content of the item (see §13.16)
- `Add-Content`: Adds content to the specified items (see §13.1)
- `Set-Content`: Writes or replaces the content in an item (see §13.47)
- `Clear-Content`: Deletes the contents of an item (see §13.3)

The type of an object that represents a directory is described in §4.5.17. The type of an object
that represents a file is described in §4.5.18.

## Path names

All items in a data store accessible through a PowerShell provider can be identified uniquely by
their path names. A *path name* is a combination of the item name, the container and subcontainers
in which the item is located, and the PowerShell drive through which the containers are accessed.

Path names are divided into one of two types: fully qualified and relative. A *fully qualified path
name* consists of all elements that make up a path. The following syntax shows the elements in a
fully qualified path name:

> [!TIP]
> The `~opt~` notation in the syntax definitions indicates that the lexical entity is optional in
> the syntax.

```Syntax
path:
    provider~opt~   drive~opt~   containers~opt~   item

provider:
    module~opt~   provider   ::

module:
    module-name   \

drive:
    drive-name   :

containers:
    container   \
    containers container   \
```

*module-name* refers to the parent module.

*provider* refers to the PowerShell provider through which the data store is accessed.

*drive* refers to the PowerShell drive that is supported by a particular PowerShell provider.

A *container* can contain other containers, which can contain other containers, and so on, with the
final container holding an *item*. Containers must be specified in the hierarchical order in which
they exist in the data store.

Here is an example of a path name:

`E:\Accounting\InvoiceSystem\Production\MasterAccount\MasterFile.dat`

If the final element in a path contains other elements, it is a *container element*; otherwise,
it's a *leaf element*.

In some cases, a fully qualified path name is not needed; a relative path name will suffice. A
*relative path name* is based on the current working location. PowerShell allows an item to be
identified based on its location relative to the current working location. A relative path name
involves the use of some special characters. The following table describes each of these characters
and provides examples of relative path names and fully qualified path names. The examples in the
table are based on the current working directory being set to C:\Windows:

| **Symbol** |              **Description**               | **Relative path**  | **Fully qualified path** |
| ---------- | ------------------------------------------ | ------------------ | ------------------------ |
| `.`        | Current working location                   | `.\System`         | `C:\Windows\System`      |
| `..`       | Parent of the current working location     | `..\Program Files` | `C:\Program Files`       |
| `\`        | Drive root of the current working location | `\Program Files`   | `C:\Program Files`       |
| none       | No special characters                      | `System`           | `C:\Windows\System`      |

To use a path name in a command, enter that name as a fully qualified or
relative path name.

The following cmdlets deal with paths:

- `Convert-Path`: Converts a path from a PowerShell path to a PowerShell provider path (see §13.8)
- `Join-Path`: Combines a path and a child path into a single path (see §13.30)
- `Resolve-Path`: Resolves the wildcard characters in a path (see §13.44)
- `Split-Path`: Returns the specified part of a path (see §13.52)
- `Test-Path`: Determines whether the elements of a path exist or if a path is well formed (see
  §13.54)

Some cmdlets (such as `Add-Content` (§13.1) and `Copy-Item` (§13.9)) use file filters. A *file
filter* is a mechanism for specifying the criteria for selecting from a set of paths.

The object type that represents a resolved path is described in §4.5.5. Paths are often manipulated
as strings.

## Scopes

### Introduction

A name can denote a variable, a function, an alias, an environment variable, or a drive. The same
name may denote different items at different places in a script. For each different item that a name
denotes, that name is visible only within the region of script text called its *scope*. Different
items denoted by the same name either have different scopes, or are in different name spaces.

Scopes may nest, in which case, an outer scope is referred to as a *parent scope,* and any nested
scopes are *child scopes* of that parent. The scope of a name is the scope in which it is defined
and all child scopes, unless it is made private. Within a child scope, a name defined there hides
any items defined with the same name in parent scopes.

Unless dot source notation (§3.5.5) is used, each of the following creates a new scope:

- A script file
- A script block
- A function or filter

Consider the following example:

```powershell
# start of script
$x = 2; $y = 3
Get-Power $x $y

#function defined in script

function Get-Power([int]$x, [int]$y)
{
if ($y -gt 0) { return $x * (Get-Power $x (--$y)) }

else { return 1 }
}
# end of script
```

The scope of the variables `$x` and `$y` created in the script is the body of that script, including the
function defined inside it. Function `Get-Power` defines two parameters with those same names. As
each function has its own scope, these variables are different from those defined in the parent
scope, and they hide those from the parent scope. The function scope is nested inside the script
scope.

Note that the function calls itself recursively. Each time it does so, it creates yet another nested
scope, each with its own variables `$x` and `$y`.

Here is a more complex example, which also shows nested scopes and reuse of names:

```powershell
# start of script scope
$x = 2              # top-level script-scope $x created
                    # $x is 2
F1                  # create nested scope with call to function F1
                    # $x is 2
F3                  # create nested scope with call to function F3
                    # $x is 2

function F1 {       # start of function scope
                    # $x is 2
    $x = $true      # function-scope $x created
                    # $x is $true

    & {             # create nested scope with script block
                    # $x is $true
        $x = 12.345 # scriptblock-scope $x created
                    # $x is 12.345
    }               # end of scriptblock scope, local $x goes away

                    # $x is $true
    F2              # create nested scope with call to function F2
                    # $x is $true
}                   # end of function scope, local $x goes away

function F2 {       # start of function scope
                    # $x is $true
    $x = "red"      # function-scope $x created
                    # $x is "red"
}                   # end of function scope, local $x goes away

function F3 {       # start of function scope
                    # $x is 2
    if ($x -gt 0) {
                    # $x is 2
        $x = "green"
                    # $x is "green"
    }               # end of block, but not end of any scope
                    # $x is still "green"
}                   # end of function scope, local $x goes away
# end of script scope
```

### Scope names and numbers

PowerShell supports the following scopes:

- Global: This is the top-most level scope. All automatic and preference variables are defined in
  this scope. The global scope is the parent scope of all other scopes, and all other scopes are
  child scopes of the global scope.

- Local: This is the current scope at any execution point within a script, script block, or
  function. Any scope can be the local scope.

- Script: This scope exists for each script file that is executed. The script scope is the parent
  scope of all scopes created from within it. A script block does *not* have its own script scope;
  instead, its script scope is that of its nearest ancestor script file. Although there is no such
  thing as module scope, script scope provides the equivalent.

Names can be declared private, in which case, they are not visible outside of their parent scope,
not even to child scopes. The concept of private is not a separate scope; it's an alias for local
scope with the addition of hiding the name if used as a writable location.

Scopes can be referred to by a number, which describes the relative position of one scope to
another. Scope 0 denotes the local scope, scope 1 denotes a 1-generation ancestor scope, scope 2
denotes a 2-generation ancestor scope, and so on. (Scope numbers are used by cmdlets that manipulate
variables.)

### Variable name scope

As shown by the following production, a variable name can be specified with any one of six different
scopes:

```Syntax
variable-scope:
    global:
    local:
    private:
    script:
    using:
    workflow:
    variable-namespace
```

The scope is optional. The following table shows the meaning of each in all possible contexts. It
also shows the scope when no scope is specified explicitly:

| **Scope Modifier** |                                  **Within a Script File**                                  |                                 **Within a Script Block**                                  |                                   **Within a Function**                                    |
| ------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| global             | Global scope                                                                               | Global scope                                                                               | Global scope                                                                               |
| script             | Nearest ancestor script file's scope or Global if there is no nearest ancestor script file | Nearest ancestor script file's scope or Global if there is no nearest ancestor script file | Nearest ancestor script file's scope or Global if there is no nearest ancestor script file |
| private            | Global/Script/Local scope                                                                  | Local scope                                                                                | Local scope                                                                                |
| local              | Global/Script/Local scope                                                                  | Local scope                                                                                | Local scope                                                                                |
| using              | Implementation defined                                                                     | Implementation defined                                                                     | Implementation defined                                                                     |
| workflow           | Implementation defined                                                                     | Implementation defined                                                                     | Implementation defined                                                                     |
| none               | Global/Script/Local scope                                                                  | Local scope                                                                                | Local scope                                                                                |

Variable scope information can also be specified when using the family of cmdlets listed in
(§3.1.5). In particular, refer to the parameter `Scope`, and the parameters `Option Private` and
`Option AllScope` for more information.

The scope `using` is used to access variables defined in another scope while running scripts via
cmdlets like `Start-Job`, `Invoke-Command`, or within an *inlinescript-statement*. For example:

```powershell
$a = 42
Invoke-Command --ComputerName RemoteServer { $using:a } # returns 42
workflow foo
{
    $b = "Hello"
    inlinescript { $using:b }
}
foo # returns "Hello"
```

The scope workflow is used with a *parallel-statement* or *sequence-statement* to access a variable
defined in the workflow.

### Function name scope

A function name may also have one of the four different scopes, and the visibility of that name is
the same as for variables (§3.5.3).

### Dot source notation

When a script file, script block, or function is executed from within another script file, script
block, or function, the executed script file creates a new nested scope. For example,

```powershell
Script1.ps1
& "Script1.ps1"
& { ... }
FunctionA
```

However, when *dot source notation* is used, no new scope is created before the command is executed,
so additions/changes it would have made to its own local scope are made to the current scope
instead. For example,

```powershell
. Script2.ps1
. "Script2.ps1"
. { ... }
. FunctionA
```

### Modules

Just like a top-level script file is at the root of a hierarchical nested scope tree, so too is each
module (§3.14). However, by default, only those names exported by a module are available by name
from within the importing context. The Global parameter of the cmdlet `Import-Module` (§13.28) allows
exported names to have increased visibility.

## ReadOnly and Constant Properties

Variables and aliases are described by objects that contain a number of properties. These properties
are set and manipulated by two families of cmdlets (§3.1.5, §3.1.1). One such property is Options,
which can be set to ReadOnly or Constant (using the Option parameter). A variable or alias marked
ReadOnly can be removed, and its properties can changed provided the Force parameter is specified.
However, a variable or alias marked Constant cannot be removed nor have its properties changed.

## Method overloads and call resolution

### Introduction

As stated in §1, an external procedure made available by the execution environment (and written in
some language other than PowerShell) is called a *method*.

The name of a method along with the number and types of its parameters are collectively called that
method's *signature*. (Note that the signature does not include the method's return type.) The
execution environment may allow a type to have multiple methods with the same name provided each has
a different signature. When multiple versions of some method are defined, that method is said to be
*overloaded*. For example, the type Math (§4.3.8) contains a set of methods called `Abs`, which
computes the absolute value of a specified number, where the specified number can have one of a
number of types. The methods in that set have the following signatures:

```powershell
Abs(decimal)
Abs(float)
Abs(double)
Abs(int)
Abs(long)
Abs(SByte)
Abs(Int16)
```

In this case, all of the methods have the same number of arguments; their signatures differ by
argument type only.

Another example involves the type Array (§4.3.2), which contains a set of methods called Copy that
copies a range of elements from one array to another, starting at the beginning of each array (by
default) or at some designated element. The methods in that set have the following signatures:

```powershell
Copy(Array, Array, int)
Copy(Array, Array, long)
Copy(Array, int, Array, int, int)
Copy(Array, long, Array, long, long)
```

In this case, the signatures differ by argument type and, in some cases, by argument number as well.

In most calls to overloaded methods, the number and type of the arguments passed exactly match one
of the overloads, and the method selected is obvious. However, if that is not the case, there needs
to be a way to resolve which overloaded version to call, if any. For example,

```powershell
[Math]::Abs([byte]10) # no overload takes type byte
[Array]::Copy($source, 3, $dest, 5L, 4) # both int and long indexes
```

Other examples include the type **string** (i.e.; **System.String**), which has numerous overloaded
methods.

Although PowerShell has rules for resolving method calls that do not match an overloaded signature
exactly, PowerShell does not itself provide a way to define overloaded methods.

> [!NOTE]
> Editor's Note: PowerShell 5.0 added the ability to define script-based classes. These classes can
> contain overloaded methods.

### Method overload resolution

Given a method call (§7.1.3) having a list of argument expressions, and a set of *candidate method*s
(i.e., those methods that could be called), the mechanism for selecting the *best method* is called
*overload resolution*.

Given the set of applicable candidate methods (§3.7.3), the best method in that set is selected. If
the set contains only one method, then that method is the best method. Otherwise, the best method is
the one method that is better than all other methods with respect to the given argument list using
the rules shown in §3.7.4. If there is not exactly one method that is better than all other methods,
then the method invocation is ambiguous and an error is reported.

The best method must be accessible in the context in which it is called. For example, a PowerShell
script cannot call a method that is private or protected.

The best method for a call to a static method must be a static method, and the best method for a
call to an instance method must be an instance method.

### Applicable method

A method is said to be *applicable* with respect to an argument list A when one of the following is
true:

- The number of arguments in A is identical to the number of parameters that the method accepts.
- The method has M required parameters and N optional parameters, and the number of arguments in A
  is greater than or equal to M, but less than N.
- The method accepts a variable number of arguments and the number of arguments in A is greater than
  the number of parameters that the method accepts.

In addition to having an appropriate number of arguments, each argument in A must match the
parameter-passing mode of the argument, and the argument type must match the parameter type, or
there must be a conversion from the argument type to the parameter type.

If the argument type is ref (§4.3.6), the corresponding parameter must also be ref, and the argument
type for conversion purposes is the type of the property Value from the ref argument.

If the argument type is `ref`, the corresponding parameter could be `out` instead of `ref`.

If the method accepts a variable number of arguments, the method may be applicable in either *normal
form* or *expanded form*. If the number of arguments in A is identical to the number of parameters
that the method accepts and the last parameter is an array, then the form depends on the rank of one
of two possible conversions:

- The rank of the conversion from the type of the last argument in A to the array type for the last
  parameter.
- The rank of the conversion from the type of the last argument in A to the element type of the
  array type for the last parameter.

If the first conversion (to the array type) is better than the second conversion (to the element
type of the array), then the method is applicable in normal form, otherwise it is applicable in
expanded form.

If there are more arguments than parameters, the method may be applicable in expanded form only. To
be applicable in expanded form, the last parameter must have array type. The method is replaced with
an equivalent method that has the last parameter replaced with sufficient parameters to account for
each unmatched argument in A. Each additional parameter type is the element type of the array type
for the last parameter in the original method. The above rules for an applicable method are applied
to this new method and argument list A.

### Better method

Given an argument list A with a set of argument expressions `{ E~1~, E~2~, ..., E~N~ }` and two
application methods `M~P~` and `M~Q~` with parameter types `{ P~1~, P~2~, ..., P~N~ }` and
`{ Q~1~, Q~2~, ..., Q~N~ }`, `M~P~` is defined to be a better method than `M~Q~` if the *cumulative
ranking of conversions* for `M~P~` is better than that for `M~Q~`.

The cumulative ranking of conversions is calculated as follows. Each conversion is worth a different
value depending on the number of parameters, with the conversion of `E~1~` worth N, `E~2~` worth
N-1, down to `E~N~` worth 1. If the conversion from `E~X~` to `P~X~` is better than that from `E~X~`
to `Q~X~`, the `M~P~` accumulates N-X+1; otherwise, `M~Q~` accumulates N-X+1. If `M~P~` and `M~Q~`
have the same value, then the following tie breaking rules are used, applied in order:

- The cumulative ranking of conversions between parameter types (ignoring argument types) is
  computed in a manner similar to the previous ranking, so `P~1~` is compared against `Q~1~`, `P~2~`
  against `Q~2~`, ..., and `P~N~` against `Q~N~`. The comparison is skipped if the argument was
  `$null`, or if the parameter types are not numeric types. The comparison is also skipped if the
  argument conversion `E~X~` loses information when converted to `P~X~` but does not lose
  information when converted to `Q~X~`, or vice versa. If the parameter conversion types are
  compared, then if the conversion from `P~X~` to `Q~X~` is better than that from `Q~X~` to `P~X~`,
  the `M~P~` accumulates N-X+1; otherwise, `M~Q~` accumulates N-X+1. This tie breaking rule is
  intended to prefer the *most specific method* (i.e., the method with parameters having the
  smallest data types) if no information is lost in conversions, or to prefer the *most general
  method* (i.e., the method with the parameters with the largest data types) if conversions result
  in loss of information.
- If both methods use their expanded form, the method with more parameters is the better method.
- If one method uses the expanded form and the other uses normal form, the method using normal form
  is the better method.

### Better conversion

The text below marked like this is specific to Windows PowerShell.

Conversions are ranked in the following manner, from lowest to highest:

- `T~1~[]` to `T~2~[]` where no assignable conversion between `T~1~` and `T~2~` exists
- T to string where T is any type
- `T~1~` to `T~2~` where `T~1~` or `T~2~` define a custom conversion in an implementation-defined manner
- `T~1~` to `T~2~` where `T~1~` implements IConvertible
- `T~1~` to `T~2~` where `T~1~` or `T~2~` implements the method `T~2~ op_Implicit(T1)`
- `T~1~` to `T~2~` where `T~1~` or `T~2~` implements the method `T~2~ op_Explicit(T1)`
- `T~1~` to `T~2~` where `T~2~` implements a constructor taking a single argument of type `T~1~`
- Either of the following conversions:
  - string to `T` where `T` implements a static method `T Parse(string)` or `T Parse(string, IFormatProvider)`
  - `T~1~` to `T~2~` where `T~2~` is any enum and `T~1~` is either string or a collection of objects that
    can be converted to string
- `T` to PSObject where `T` is any type
- Any of the following conversions: `Language`
  - T to bool where `T` is any numeric type
  - string to `T` where `T` is `regex`, `wmisearcher`, `wmi`, `wmiclass`, `adsi`, `adsisearcher`, or
    `type`
  - `T` to `bool`
  - T~1~ to `Nullable[T~2~]` where a conversion from `T~1~` to `T~2~` exists
  - `T` to void
  - `T~1~[]` to `T~2~[]` where an assignable conversion between `T~1~` and `T~2~` exists
  - `T~1~` to `T~2~[]` where `T~1~` is a collection
  - `IDictionary` to `Hashtable`
  - `T` to `ref`
  - `T` to `xml`
  - `scriptblock` to `delegate`
  - `T~1~` to `T~2~` where `T~1~` is an integer type and `T~2~` is an enum
- `$null` to `T` where `T` is any value type
- `$null` to `T` where `T` is any reference type
- Any of the following conversions:
  - byte to `T` where `T` is `SByte`

  - `UInt16` to `T` where `T` is `SByte`, `byte`, or `Int16`
  - `Int16` to `T` where `T` is `SByte` or `byte`
  - `UInt32` to `T` where `T` is `SByte`, `byte`, `Int16`, `UInt16`, or `int`
  - `int` to `T` where `T` is `SByte`, `byte`, `Int16`, or `UInt16`
  - `UInt64` to `T` where `T` is `SByte`, `byte`, `Int16`, `UInt16`, `int`, `UInt32`, or `long`
  - `long` to `T` where `T` is `SByte`, `byte`, `Int16`, `UInt16`, `int`, or `UInt32`
  - `float` to `T` where `T` is any integer type or `decimal`
  - `double` to `T` where `T` is any integer type or `decimal`
  - `decimal` to `T` where `T` is any integer type
- Any of the following conversions:
  - `SByte` to `T` where `T` is `byte`, `uint6`, `UInt32`, or `UInt64`
  - `Int16` to `T` where `T` is `UInt16`, `UInt32`, or `UInt64`
  - `int` to `T` where `T` is `UInt32` or `UInt64`
  - `long` to `UInt64`
  - `decimal` to `T` where `T` is `float` or `double`
- Any of the following conversions:
  - `T` to `string` where `T` is any numeric type
  - `T` to `char` where `T` is any numeric type
  - `string` to `T` where `T` is any numeric type
- Any of the following conversions, these conversion are considered an assignable conversions:
  - `byte` to `T` where `T` is `Int16`, `UInt16`, `int`, `UInt32`, `long`, `UInt64`, `single`,
    `double`, or `decimal`
  - `SByte` to `T` where `T` is `Int16`, `UInt16`, `int`, `UInt32`, `long`, `UInt64`, `single`,
    `double`, or `decimal`
  - `UInt16` to `T` where `T` is `int`, `UInt32`, `long`, or `UInt64`, `single`, `double`, or
    `decimal`
  - `Int16` to `T` where `T` is `int`, `UInt32`, `long`, or `UInt64`, `single`, `double`, or
    `decimal`
  - `UInt32` to `T` where `T` is `long`, or `UInt64`, `single`, `double`, or `decimal`
  - `int` to `T` where `T` is `long`, `UInt64`, `single`, `double`, or `decimal`
  - `single` to `double`
- `T~1~` to `T~2~` where `T~2~` is a base class or interface of `T~1~`. This conversion is considered an
  assignable conversion.
- `string` to `char[]`
- `T` to `T` -- This conversion is considered an assignable conversion.

For each conversion of the form `T~1~` to `T~2~[]` where `T~1~` is not an array and no other
conversion applies, if there is a conversion from `T~1~` to `T~2~`, the rank of the conversion is
worse than the conversion from `T~1~` to `T~2~`, but better than any conversion ranked less than the
conversion from `T~1~` to `T~2~`

## Name lookup

It is possible to have commands of different kinds all having the same name. The order in which name
lookup is performed in such a case is alias, function, cmdlet, and external command.

## Type name lookup

§7.1.10 contains the statement, "A *type-literal* is represented in an implementation by some
unspecified *underlying type*. As a result, a type name is a synonym for its underlying type."
Example of types are `int`, `double`, `long[]`, and `Hashtable`.

Type names are matched as follows: Compare a given type name with the list of built-in *type
accelerators*, such as int, long, double. If a match is found, that is the type. Otherwise, presume
the type name is fully qualified and see if such a type exists on the host system. If a match is
found, that is the type. Otherwise, add the namespace prefix `System.`. If a match is found, that is
the type. Otherwise, the type name is in error. This algorithm is applied for each type argument for
generic types. However, there is no need to specify the arity (the number of arguments or operands
taken by a function or operator).

## Automatic memory management

Various operators and cmdlets result in the allocation of memory for reference-type objects, such as
strings and arrays. The allocation and freeing of this memory is managed by the PowerShell runtime
system. That is, PowerShell provides automatic *garbage collection*.

## Execution order

A *side effect* is a change in the state of a command's execution environment. A change to the
value of a variable (via the assignment operators or the pre- and post-increment and decrement
operators) is a side effect, as is a change to the contents of a file.

Unless specified otherwise, statements are executed in lexical order.

Except as specified for some operators, the order of evaluation of terms in an expression and the
order in which side effects take place are both unspecified.

An expression that invokes a command involves the expression that designates the command, and zero
or more expressions that designate the arguments whose values are to be passed to that command. The
order in which these expressions are evaluated relative to each other is unspecified.

## Error handling

When a command fails, this is considered an *error*, and information about that error is recorded in
an *error record*, whose type is unspecified (§4.5.15); however, this type supports subscripting.

An error falls into one of two categories. Either it terminates the operation (a *terminating
error*) or it doesn't (a *non-terminating error*). With a terminating error, the error is recorded
and the operation stops. With a non-terminating error, the error is recorded and the operation
continues.

Non-terminating errors are written to the error stream. Although that information can be redirected
to a file, the error objects are first converted to strings and important information in those
objects would not be captured making diagnosis difficult if not impossible. Instead, the error text
can be redirected (§7.12) and the error object saved in a variable, as in `$Error1 = command 2>&1`.

The automatic variable `$Error` contains a collection of error records that represent recent errors,
and the most recent error is in `$Error[0]`. This collection is maintained in a buffer such that
old records are discarded as new ones are added. The automatic variable `$MaximumErrorCount` controls
the number of records that can be stored.

`$Error` contains all of the errors from all commands mixed in together in one collection. To collect
the errors from a specific command, use the common parameter ErrorVariable (§13.56), which allows a
user-defined variable to be specified to hold the collection.

## Pipelines

A *pipeline* is a series of one or more commands each separated by the pipe operator `|` (U+007C).
Each command receives input from its predecessor and writes output to its successor. Unless the
output at the end of the pipeline is discarded or redirected to a file, it is sent to the host
environment, which may choose to write it to standard output. Commands in a pipeline may also
receive input from arguments. For example, consider the following use of commands `Get-ChildItem`,
`Sort-Object`, and `Process-File`, which create a list of file names in a given file system
directory, sort a set of text records, and perform some processing on a text record, respectively:

```powershell
Get-ChildItem
Get-ChildItem e:*.txt | Sort-Object -CaseSensitive | Process-File >results.txt
```

In the first case, `Get-ChildItem` creates a collection of names of the files in the current/default
directory. That collection is sent to the host environment, which, by default, writes each
element's value to standard output.

In the second case, `Get-ChildItem` creates a collection of names of the files in the directory
specified, using the argument `e:*.txt`. That collection is written to the command `Sort-Object`,
which, by default, sorts them in ascending order, sensitive to case (by virtue of the
**CaseSensitive** argument). The resulting collection is then written to command `Process-File`,
which performs some (unknown) processing. The output from that command is then redirected to the
file `results.txt`.

If a command writes a single object, its successor receives that object and then terminates after
writing its own object(s) to its successor. If, however, a command writes multiple objects, they are
delivered one at a time to the successor command, which executes once per object. This behavior is
called *streaming*. In stream processing, objects are written along the pipeline as soon as they
become available, not when the entire collection has been produced.

When processing a collection, a command can be written such that it can do special processing before
the initial element and after the final element.

## Modules

A *module* is a self-contained reusable unit that allows PowerShell code to be partitioned,
organized, and abstracted. A module can contain commands (such as cmdlets and functions) and items
(such as variables and aliases) that can be used as a single unit.

Once a module has been created, it must be *imported* into a session before the commands and items
within it can be used. Once imported, commands and items behave as if they were defined locally. A
module is imported explicitly with the `Import-Module` (§13.28) command. A module may also be
imported automatically as determined in an implementation defined manner.

The type of an object that represents a module is described in §4.5.12.

Modules are discussed in detail in §11.

## Wildcard expressions

A wildcard expression may contain zero or more of the following elements:

<table>
<thead>
<tr class="header">
<th>Element</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Character other than *, ?, or [</td>
<td>Matches that one character</td>
</tr>
<tr class="even">
<td>*</td>
<td>Matches zero or more characters. To match a * character, use [*].</td>
</tr>
<tr class="odd">
<td>?</td>
<td>Matches any one character. To match a ? character, use [?].</td>
</tr>
<tr class="even">
<td>[<em>set</em>]</td>
<td><p>Matches any one character from <em>set</em>, which cannot be empty.</p>
<p>If <em>set</em> begins with ], that right square bracket is considered part of <em>set</em> and the next right square bracket terminates the set; otherwise, the first right square bracket terminates the set.</p>
<p>If <em>set</em> begins or ends with -, that hyphen-minus is considered part of <em>set</em>; otherwise, it indicates a range of consecutive Unicode code points with the characters either side of the hyphen-minus being the inclusive range delimiters. For example, A-Z indicates the 26 uppercase English letters, and 0-9 indicates the 10 decimal digits.</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> More information can be found in,
> [The Open Group Base Specifications: Pattern Matching", IEEE Std 1003.1, 2004 Edition.](http://www.opengroup.org/onlinepubs/000095399/utilities/xcu_chap02.html#tag_02_13_01).
> However, in PowerShell, the escape character is backtick, not backslash.

## Regular expressions

A regular expression may contain zero or more of the following elements:

<table>
<thead>
<tr class="header">
<th>Element</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Character other than ., [, ^, *, $, or \</td>
<td>Matches that one character</td>
</tr>
<tr class="even">
<td>.</td>
<td>Matches any one character. To match a . character, use \..</td>
</tr>
<tr class="odd">
<td>[<em>set</em>]<br />
[^<em>set</em>]</td>
<td><p>The [<em>set</em>] form matches any one character from <em>set</em>. The [^<em>set</em>] form matches no characters from <em>set</em>. <em>set</em> cannot be empty.</p>
<p>If <em>set</em> begins with ] or ^], that right square bracket is considered part of <em>set</em> and the next right square bracket terminates the set; otherwise, the first right square bracket terminates the set.</p>
<p>If <em>set</em> begins with - or ^-, or ends with -, that hyphen-minus is considered part of <em>set</em>; otherwise, it indicates a range of consecutive Unicode code points with the characters either side of the hyphen-minus being the inclusive range delimiters. For example, A-Z indicates the 26 uppercase English letters, and 0-9 indicates the 10 decimal digits.</p></td>
</tr>
<tr class="even">
<td>*</td>
<td>Matches zero of more occurrences of the preceding element.</td>
</tr>
<tr class="odd">
<td>+</td>
<td>Matches one of more occurrences of the preceding element.</td>
</tr>
<tr class="even">
<td>?</td>
<td>Matches zero of one occurrences of the preceding element.</td>
</tr>
<tr class="odd">
<td>^</td>
<td>Matches at the start of the string. To match a ^ character, use \^.</td>
</tr>
<tr class="even">
<td>$</td>
<td>Matches at the end of the string. To match a $ character, use $.</td>
</tr>
<tr class="odd">
<td>\<em>c</em></td>
<td>Escapes character <em>c</em>, so it isn't recognized as a regular expression element.</td>
</tr>
</tbody>
</table>

> [!NOTE]
> More information can be found in,
> [The Open Group Base Specifications: Regular Expressions, IEEE Std 1003.1, 2004 Edition.](http://www.opengroup.org/onlinepubs/000095399/basedefs/xbd_chap09.html).

Windows PowerShell: Character classes available in Microsoft .NET Framework regular expressions are
supported, as follows:

|  Element   |                                                                                                            Description                                                                                                             |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `\p{name}` | Matches any character in the named character class specified by *name*. Supported names are Unicode groups and block ranges such as Ll, Nd, Z, IsGreek, and IsBoxDrawing.                                                          |
| `\P{name}` | Matches text not included in the groups and block ranges specified in *name*.                                                                                                                                                      |
| `\w`       | Matches any word character. Equivalent to the Unicode character categories `[\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}]`. If ECMAScript-compliant behavior is specified with the ECMAScript option, \w is equivalent to `[a-zA-Z_0-9]`. |
| `\W`       | Matches any non-word character. Equivalent to the Unicode categories `[\^\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}]`.                                                                                                                   |
| `\s`       | Matches any white space character. Equivalent to the Unicode character categories` [\f\n\r\t\v\x85\p{Z}]`.                                                                                                                         |
| `\S`       | Matches any non-white-space character. Equivalent to the Unicode character categories `[\^\f\n\r\t\v\x85\p{Z}]`.                                                                                                                   |
| `\d`       | Matches any decimal digit. Equivalent to `\p{Nd}` for Unicode and `[0-9]` for non-Unicode behavior.                                                                                                                                |
| `\D`       | Matches any non-digit. Equivalent to `\P{Nd}` for Unicode and `[\^0-9]` for non-Unicode behavior.                                                                                                                                  |

Quantifiers available in Microsoft .NET Framework regular expressions are supported, as follows:

| Element |                                      Description                                      |
| ------- | ------------------------------------------------------------------------------------- |
| `*`     | Specifies zero or more matches; for example, `\w* `or `(abc)*.` Equivalent to `{0,}`. |
| `+`     | Matches repeating instances of the preceding characters.                              |
| `?`     | Specifies zero or one matches; for example, `\w?` or `(abc)?`. Equivalent to `{0,1}`. |
| `{n}`   | Specifies exactly *n* matches; for example, `(pizza){2}`.                             |
| `{n,}`  | Specifies at least *n* matches; for example, `(abc){2,}`.                             |
| `{n,m}` | Specifies at least *n*, but no more than *m*, matches.                                |