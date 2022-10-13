```yaml
title: Bash scripting
category: CLI
layout: 2022/sheet
tags: [Featured]
updated: 11-Oct-2022
keywords:
  - Variables
  - Functions
  - Interpolation
  - Brace expansions
  - Loops
  - Conditional execution
  - Command substitution
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Introduction](#Introduction)
* 2. [Example](#Example)
* 3. [Variables](#Variables)
* 4. [String quotes](#Stringquotes)
* 5. [Shell execution](#Shellexecution)
* 6. [Conditional execution](#Conditionalexecution)
* 7. [Functions](#Functions)
* 8. [Conditionals](#Conditionals)
* 9. [Strict mode](#Strictmode)
* 10. [Brace expansion](#Braceexpansion)
* 11. [Basics](#Basics)
* 12. [Substitution](#Substitution)
* 13. [Comments](#Comments)
* 14. [Substrings](#Substrings)
* 15. [Length](#Length)
* 16. [Manipulation](#Manipulation)
* 17. [Default values](#Defaultvalues)
* 18. [Basic for loop](#Basicforloop)
* 19. [C-like for loop](#C-likeforloop)
* 20. [Ranges](#Ranges)
  * 20.1. [With step size](#Withstepsize)
* 21. [Reading lines](#Readinglines)
* 22. [Forever](#Forever)
* 23. [Defining functions](#Definingfunctions)
* 24. [Returning values](#Returningvalues)
* 25. [Raising errors](#Raisingerrors)
* 26. [Arguments](#Arguments)
* 27. [Conditions](#Conditions)
  * 27.1. [More conditions](#Moreconditions)
* 28. [File conditions](#Fileconditions)
* 29. [Example](#Example-1)
* 30. [Defining arrays](#Definingarrays)
* 31. [Working with arrays](#Workingwitharrays)
* 32. [Operations](#Operations)
* 33. [Iteration](#Iteration)
* 34. [Defining](#Defining)
* 35. [Working with dictionaries](#Workingwithdictionaries)
* 36. [Iteration](#Iteration-1)
  * 36.1. [Iterate over values](#Iterateovervalues)
  * 36.2. [Iterate over keys](#Iterateoverkeys)
* 37. [Options](#Options)
* 38. [Glob options](#Globoptions)
* 39. [Commands](#Commands)
* 40. [Expansions](#Expansions)
* 41. [Operations](#Operations-1)
* 42. [Slices](#Slices)
* 43. [Numeric calculations](#Numericcalculations)
* 44. [Subshells](#Subshells)
* 45. [Redirection](#Redirection)
* 46. [Inspecting commands](#Inspectingcommands)
* 47. [Trap errors](#Traperrors)
* 48. [Case/switch](#Caseswitch)
* 49. [Source relative](#Sourcerelative)
* 50. [printf](#printf)
* 51. [Transform strings](#Transformstrings)
  * 51.1. [Example](#Example-1)
* 52. [Directory of script](#Directoryofscript)
* 53. [Getting options](#Gettingoptions)
* 54. [Heredoc](#Heredoc)
* 55. [Reading input](#Readinginput)
* 56. [Special variables](#Specialvariables)
* 57. [Go to previous directory](#Gotopreviousdirectory)
* 58. [Check for command's result](#Checkforcommandsresult)
* 59. [Grep check](#Grepcheck)
* 60. [Also see](#Alsosee)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->


###  1. <a name='Introduction'></a>Introduction


This is a quick reference to getting started with Bash scripting.

- [Explain Shell](https://explainshell.com/) _(explainshell.com)_
- [Learn bash in y minutes](https://learnxinyminutes.com/docs/bash/) _(learnxinyminutes.com)_
- [Bash Guide](http://mywiki.wooledge.org/BashGuide) _(mywiki.wooledge.org)_
- [Bash Hackers Wiki](https://wiki.bash-hackers.org) _(wiki.bash-hackers.org)_

###  2. <a name='Example'></a>Example

```bash
#!/usr/bin/env bash

NAME="John"
echo "Hello $NAME!"
```

###  3. <a name='Variables'></a>Variables

```bash
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}!"
```

###  4. <a name='Stringquotes'></a>String quotes

```bash
NAME="John"
echo "Hi $NAME"  #=> Hi John
echo 'Hi $NAME'  #=> Hi $NAME
```

###  5. <a name='Shellexecution'></a>Shell execution

```bash
echo "I'm in $(pwd)"
echo "I'm in `pwd`"
# Same
```

See [Command substitution](http://wiki.bash-hackers.org/syntax/expansion/cmdsubst)

###  6. <a name='Conditionalexecution'></a>Conditional execution

```bash
git commit && git push
git commit || echo "Commit failed"
```

###  7. <a name='Functions'></a>Functions

```bash
get_name() {
  echo "John"
}

echo "You are $(get_name)"
```

See: [Functions](#functions)

###  8. <a name='Conditionals'></a>Conditionals

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

See: [Conditionals](#conditionals)

###  9. <a name='Strictmode'></a>Strict mode

```bash
set -euo pipefail
IFS=$'\n\t'
```

See: [Unofficial bash strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)

###  10. <a name='Braceexpansion'></a>Brace expansion

```bash
echo {A,B}.js
```

| Expression | Description         |
| ---------- | ------------------- |
| `{A,B}`    | Same as `A B`       |
| `{A,B}.js` | Same as `A.js B.js` |
| `{1..5}`   | Same as `1 2 3 4 5` |

See: [Brace expansion](http://wiki.bash-hackers.org/syntax/expansion/brace)


Parameter expansions
--------------------


###  11. <a name='Basics'></a>Basics

```bash
name="John"
echo ${name}
echo ${name/J/j}    #=> "john" (substitution)
echo ${name:0:2}    #=> "Jo" (slicing)
echo ${name::2}     #=> "Jo" (slicing)
echo ${name::-1}    #=> "Joh" (slicing)
echo ${name:(-1)}   #=> "n" (slicing from right)
echo ${name:(-2):1} #=> "h" (slicing from right)
echo ${food:-Cake}  #=> $food or "Cake"
```

```bash
length=2
echo ${name:0:length}  #=> "Jo"
```

See: [Parameter expansion](http://wiki.bash-hackers.org/syntax/pe)

```bash
STR="/path/to/foo.cpp"
echo ${STR%.cpp}    # /path/to/foo
echo ${STR%.cpp}.o  # /path/to/foo.o
echo ${STR%/*}      # /path/to

echo ${STR##*.}     # cpp (extension)
echo ${STR##*/}     # foo.cpp (basepath)

echo ${STR#*/}      # path/to/foo.cpp
echo ${STR##*/}     # foo.cpp

echo ${STR/foo/bar} # /path/to/bar.cpp
```

```bash
STR="Hello world"
echo ${STR:6:5}   # "world"
echo ${STR: -5:5}  # "world"
```

```bash
SRC="/path/to/foo.cpp"
BASE=${SRC##*/}   #=> "foo.cpp" (basepath)
DIR=${SRC%$BASE}  #=> "/path/to/" (dirpath)
```

###  12. <a name='Substitution'></a>Substitution

| Code              | Description         |
| ----------------- | ------------------- |
| `${FOO%suffix}`   | Remove suffix       |
| `${FOO#prefix}`   | Remove prefix       |
| ---               | ---                 |
| `${FOO%%suffix}`  | Remove long suffix  |
| `${FOO##prefix}`  | Remove long prefix  |
| ---               | ---                 |
| `${FOO/from/to}`  | Replace first match |
| `${FOO//from/to}` | Replace all         |
| ---               | ---                 |
| `${FOO/%from/to}` | Replace suffix      |
| `${FOO/#from/to}` | Replace prefix      |

###  13. <a name='Comments'></a>Comments

```bash
# Single line comment
```

```bash
: '
This is a
multi line
comment
'
```

###  14. <a name='Substrings'></a>Substrings

| Expression      | Description                    |
| --------------- | ------------------------------ |
| `${FOO:0:3}`    | Substring _(position, length)_ |
| `${FOO:(-3):3}` | Substring from the right       |

###  15. <a name='Length'></a>Length

| Expression | Description      |
| ---------- | ---------------- |
| `${#FOO}`  | Length of `$FOO` |

###  16. <a name='Manipulation'></a>Manipulation

```bash
STR="HELLO WORLD!"
echo ${STR,}   #=> "hELLO WORLD!" (lowercase 1st letter)
echo ${STR,,}  #=> "hello world!" (all lowercase)

STR="hello world!"
echo ${STR^}   #=> "Hello world!" (uppercase 1st letter)
echo ${STR^^}  #=> "HELLO WORLD!" (all uppercase)
```

###  17. <a name='Defaultvalues'></a>Default values

| Expression        | Description                                              |
| ----------------- | -------------------------------------------------------- |
| `${FOO:-val}`     | `$FOO`, or `val` if unset (or null)                      |
| `${FOO:=val}`     | Set `$FOO` to `val` if unset (or null)                   |
| `${FOO:+val}`     | `val` if `$FOO` is set (and not null)                    |
| `${FOO:?message}` | Show error message and exit if `$FOO` is unset (or null) |

Omitting the `:` removes the (non)nullity checks, e.g. `${FOO-val}` expands to `val` if unset otherwise `$FOO`.

Loops
-----


###  18. <a name='Basicforloop'></a>Basic for loop

```bash
for i in /etc/rc.*; do
  echo $i
done
```

###  19. <a name='C-likeforloop'></a>C-like for loop

```bash
for ((i = 0 ; i < 100 ; i++)); do
  echo $i
done
```

###  20. <a name='Ranges'></a>Ranges

```bash
for i in {1..5}; do
    echo "Welcome $i"
done
```

####  20.1. <a name='Withstepsize'></a>With step size

```bash
for i in {5..50..5}; do
    echo "Welcome $i"
done
```

###  21. <a name='Readinglines'></a>Reading lines

```bash
cat file.txt | while read line; do
  echo $line
done
```

###  22. <a name='Forever'></a>Forever

```bash
while true; do
  ···
done
```

Functions
---------


###  23. <a name='Definingfunctions'></a>Defining functions

```bash
myfunc() {
    echo "hello $1"
}
```

```bash
# Same as above (alternate syntax)
function myfunc() {
    echo "hello $1"
}
```

```bash
myfunc "John"
```

###  24. <a name='Returningvalues'></a>Returning values

```bash
myfunc() {
    local myresult='some value'
    echo $myresult
}
```

```bash
result="$(myfunc)"
```

###  25. <a name='Raisingerrors'></a>Raising errors

```bash
myfunc() {
  return 1
}
```

```bash
if myfunc; then
  echo "success"
else
  echo "failure"
fi
```

###  26. <a name='Arguments'></a>Arguments

| Expression | Description                                      |
| ---        | ---                                              |
| `$#`       | Number of arguments                              |
| `$*`       | All positional arguments  (as a single word)     |
| `$@`       | All positional arguments (as separate strings)  |
| `$1`       | First argument                                   |
| `$_`       | Last argument of the previous command            |

**Note**: `$@` and `$*` must be quoted in order to perform as described.
Otherwise, they do exactly the same thing (arguments as separate strings).

See [Special parameters](http://wiki.bash-hackers.org/syntax/shellvars#special_parameters_and_shell_variables).

Conditionals
------------


###  27. <a name='Conditions'></a>Conditions

Note that `[[` is actually a command/program that returns either `0` (true) or `1` (false). Any program that obeys the same logic (like all base utils, such as `grep(1)` or `ping(1)`) can be used as condition, see examples.

| Condition                | Description           |
| ---                      | ---                   |
| `[[ -z STRING ]]`        | Empty string          |
| `[[ -n STRING ]]`        | Not empty string      |
| `[[ STRING == STRING ]]` | Equal                 |
| `[[ STRING != STRING ]]` | Not Equal             |
| ---                      | ---                   |
| `[[ NUM -eq NUM ]]`      | Equal                 |
| `[[ NUM -ne NUM ]]`      | Not equal             |
| `[[ NUM -lt NUM ]]`      | Less than             |
| `[[ NUM -le NUM ]]`      | Less than or equal    |
| `[[ NUM -gt NUM ]]`      | Greater than          |
| `[[ NUM -ge NUM ]]`      | Greater than or equal |
| ---                      | ---                   |
| `[[ STRING =~ STRING ]]` | Regexp                |
| ---                      | ---                   |
| `(( NUM < NUM ))`        | Numeric conditions    |

####  27.1. <a name='Moreconditions'></a>More conditions

| Condition            | Description              |
| -------------------- | ------------------------ |
| `[[ -o noclobber ]]` | If OPTIONNAME is enabled |
| ---                  | ---                      |
| `[[ ! EXPR ]]`       | Not                      |
| `[[ X && Y ]]`       | And                      |
| `[[ X || Y ]]`       | Or                       |

###  28. <a name='Fileconditions'></a>File conditions

| Condition               | Description             |
| ---                     | ---                     |
| `[[ -e FILE ]]`         | Exists                  |
| `[[ -r FILE ]]`         | Readable                |
| `[[ -h FILE ]]`         | Symlink                 |
| `[[ -d FILE ]]`         | Directory               |
| `[[ -w FILE ]]`         | Writable                |
| `[[ -s FILE ]]`         | Size is > 0 bytes       |
| `[[ -f FILE ]]`         | File                    |
| `[[ -x FILE ]]`         | Executable              |
| ---                     | ---                     |
| `[[ FILE1 -nt FILE2 ]]` | 1 is more recent than 2 |
| `[[ FILE1 -ot FILE2 ]]` | 2 is more recent than 1 |
| `[[ FILE1 -ef FILE2 ]]` | Same files              |

###  29. <a name='Example-1'></a>Example

```bash
# String
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
else
  echo "This never happens"
fi
```

```bash
# Combinations
if [[ X && Y ]]; then
  ...
fi
```

```bash
# Equal
if [[ "$A" == "$B" ]]
```

```bash
# Regex
if [[ "A" =~ . ]]
```

```bash
if (( $a < $b )); then
   echo "$a is smaller than $b"
fi
```

```bash
if [[ -e "file.txt" ]]; then
  echo "file exists"
fi
```

Arrays
------

###  30. <a name='Definingarrays'></a>Defining arrays

```bash
Fruits=('Apple' 'Banana' 'Orange')
```

```bash
Fruits[0]="Apple"
Fruits[1]="Banana"
Fruits[2]="Orange"
```

###  31. <a name='Workingwitharrays'></a>Working with arrays

```bash
echo ${Fruits[0]}           # Element #0
echo ${Fruits[-1]}          # Last element
echo ${Fruits[@]}           # All elements, space-separated
echo ${#Fruits[@]}          # Number of elements
echo ${#Fruits}             # String length of the 1st element
echo ${#Fruits[3]}          # String length of the Nth element
echo ${Fruits[@]:3:2}       # Range (from position 3, length 2)
echo ${!Fruits[@]}          # Keys of all elements, space-separated
```

###  32. <a name='Operations'></a>Operations

```bash
Fruits=("${Fruits[@]}" "Watermelon")    # Push
Fruits+=('Watermelon')                  # Also Push
Fruits=( ${Fruits[@]/Ap*/} )            # Remove by regex match
unset Fruits[2]                         # Remove one item
Fruits=("${Fruits[@]}")                 # Duplicate
Fruits=("${Fruits[@]}" "${Veggies[@]}") # Concatenate
lines=(`cat "logfile"`)                 # Read from file
```

###  33. <a name='Iteration'></a>Iteration

```bash
for i in "${arrayName[@]}"; do
  echo $i
done
```

Dictionaries
------------


###  34. <a name='Defining'></a>Defining

```bash
declare -A sounds
```

```bash
sounds[dog]="bark"
sounds[cow]="moo"
sounds[bird]="tweet"
sounds[wolf]="howl"
```

Declares `sound` as a Dictionary object (aka associative array).

###  35. <a name='Workingwithdictionaries'></a>Working with dictionaries

```bash
echo ${sounds[dog]} # Dog's sound
echo ${sounds[@]}   # All values
echo ${!sounds[@]}  # All keys
echo ${#sounds[@]}  # Number of elements
unset sounds[dog]   # Delete dog
```

###  36. <a name='Iteration-1'></a>Iteration

####  36.1. <a name='Iterateovervalues'></a>Iterate over values

```bash
for val in "${sounds[@]}"; do
  echo $val
done
```

####  36.2. <a name='Iterateoverkeys'></a>Iterate over keys

```bash
for key in "${!sounds[@]}"; do
  echo $key
done
```

Options
-------

###  37. <a name='Options'></a>Options

```bash
set -o noclobber  # Avoid overlay files (echo "hi" > foo)
set -o errexit    # Used to exit upon error, avoiding cascading errors
set -o pipefail   # Unveils hidden failures
set -o nounset    # Exposes unset variables
```

###  38. <a name='Globoptions'></a>Glob options

```bash
shopt -s nullglob    # Non-matching globs are removed  ('*.foo' => '')
shopt -s failglob    # Non-matching globs throw errors
shopt -s nocaseglob  # Case insensitive globs
shopt -s dotglob     # Wildcards match dotfiles ("*.sh" => ".foo.sh")
shopt -s globstar    # Allow ** for recursive matches ('lib/**/*.rb' => 'lib/a/b/c.rb')
```

Set `GLOBIGNORE` as a colon-separated list of patterns to be removed from glob
matches.

History
-------

###  39. <a name='Commands'></a>Commands

| Command               | Description                               |
| --------------------- | ----------------------------------------- |
| `history`             | Show history                              |
| `shopt -s histverify` | Don't execute expanded result immediately |

###  40. <a name='Expansions'></a>Expansions

| Expression   | Description                                          |
| ------------ | ---------------------------------------------------- |
| `!$`         | Expand last parameter of most recent command         |
| `!*`         | Expand all parameters of most recent command         |
| `!-n`        | Expand `n`th most recent command                     |
| `!n`         | Expand `n`th command in history                      |
| `!<command>` | Expand most recent invocation of command `<command>` |

###  41. <a name='Operations-1'></a>Operations

| Code                 | Description                                                           |
| -------------------- | --------------------------------------------------------------------- |
| `!!`                 | Execute last command again                                            |
| `!!:s/<FROM>/<TO>/`  | Replace first occurrence of `<FROM>` to `<TO>` in most recent command |
| `!!:gs/<FROM>/<TO>/` | Replace all occurrences of `<FROM>` to `<TO>` in most recent command  |
| `!$:t`               | Expand only basename from last parameter of most recent command       |
| `!$:h`               | Expand only directory from last parameter of most recent command      |

`!!` and `!$` can be replaced with any valid expansion.

###  42. <a name='Slices'></a>Slices

| Code     | Description                                                                              |
| -------- | ---------------------------------------------------------------------------------------- |
| `!!:n`   | Expand only `n`th token from most recent command (command is `0`; first argument is `1`) |
| `!^`     | Expand first argument from most recent command                                           |
| `!$`     | Expand last token from most recent command                                               |
| `!!:n-m` | Expand range of tokens from most recent command                                          |
| `!!:n-$` | Expand `n`th token to last from most recent command                                      |

`!!` can be replaced with any valid expansion i.e. `!cat`, `!-2`, `!42`, etc.


Miscellaneous
-------------

###  43. <a name='Numericcalculations'></a>Numeric calculations

```bash
$((a + 200))      # Add 200 to $a
```

```bash
$(($RANDOM%200))  # Random number 0..199
```

###  44. <a name='Subshells'></a>Subshells

```bash
(cd somedir; echo "I'm now in $PWD")
pwd # still in first directory
```

###  45. <a name='Redirection'></a>Redirection

```bash
python hello.py > output.txt   # stdout to (file)
python hello.py >> output.txt  # stdout to (file), append
python hello.py 2> error.log   # stderr to (file)
python hello.py 2>&1           # stderr to stdout
python hello.py 2>/dev/null    # stderr to (null)
python hello.py &>/dev/null    # stdout and stderr to (null)
```

```bash
python hello.py < foo.txt      # feed foo.txt to stdin for python
diff <(ls -r) <(ls)            # Compare two stdout without files
```

###  46. <a name='Inspectingcommands'></a>Inspecting commands

```bash
command -V cd
#=> "cd is a function/alias/whatever"
```

###  47. <a name='Traperrors'></a>Trap errors

```bash
trap 'echo Error at about $LINENO' ERR
```

or

```bash
traperr() {
  echo "ERROR: ${BASH_SOURCE[1]} at about ${BASH_LINENO[0]}"
}

set -o errtrace
trap traperr ERR
```

###  48. <a name='Caseswitch'></a>Case/switch

```bash
case "$1" in
  start | up)
    vagrant up
    ;;

  *)
    echo "Usage: $0 {start|stop|ssh}"
    ;;
esac
```

###  49. <a name='Sourcerelative'></a>Source relative

```bash
source "${0%/*}/../share/foo.sh"
```

###  50. <a name='printf'></a>printf

```bash
printf "Hello %s, I'm %s" Sven Olga
#=> "Hello Sven, I'm Olga

printf "1 + 1 = %d" 2
#=> "1 + 1 = 2"

printf "This is how you print a float: %f" 2
#=> "This is how you print a float: 2.000000"
```

###  51. <a name='Transformstrings'></a>Transform strings

| Command option     | Description                                         |
| ------------------ | --------------------------------------------------- |
| `-c`               | Operations apply to characters not in the given set |
| `-d`               | Delete characters                                   |
| `-s`               | Replaces repeated characters with single occurrence |
| `-t`               | Truncates                                           |
| `[:upper:]`        | All upper case letters                              |
| `[:lower:]`        | All lower case letters                              |
| `[:digit:]`        | All digits                                          |
| `[:space:]`        | All whitespace                                      |
| `[:alpha:]`        | All letters                                         |
| `[:alnum:]`        | All letters and digits                              |

####  51.1. <a name='Example-1'></a>Example

```bash
echo "Welcome To Devhints" | tr [:lower:] [:upper:]
WELCOME TO DEVHINTS
```

###  52. <a name='Directoryofscript'></a>Directory of script

```bash
DIR="${0%/*}"
```

###  53. <a name='Gettingoptions'></a>Getting options

```bash
while [[ "$1" =~ ^- && ! "$1" == "--" ]]; do case $1 in
  -V | --version )
    echo $version
    exit
    ;;
  -s | --string )
    shift; string=$1
    ;;
  -f | --flag )
    flag=1
    ;;
esac; shift; done
if [[ "$1" == '--' ]]; then shift; fi
```

###  54. <a name='Heredoc'></a>Heredoc

```sh
cat <<END
hello world
END
```

###  55. <a name='Readinginput'></a>Reading input

```bash
echo -n "Proceed? [y/n]: "
read ans
echo $ans
```

```bash
read -n 1 ans    # Just one character
```

###  56. <a name='Specialvariables'></a>Special variables

| Expression         | Description                            |
| ------------------ | -------------------------------------- |
| `$?`               | Exit status of last task               |
| `$!`               | PID of last background task            |
| `$$`               | PID of shell                           |
| `$0`               | Filename of the shell script           |
| `$_`               | Last argument of the previous command  |
| `${PIPESTATUS[n]}` | return value of piped commands (array) |

See [Special parameters](http://wiki.bash-hackers.org/syntax/shellvars#special_parameters_and_shell_variables).

###  57. <a name='Gotopreviousdirectory'></a>Go to previous directory

```bash
pwd # /home/user/foo
cd bar/
pwd # /home/user/foo/bar
cd -
pwd # /home/user/foo
```

###  58. <a name='Checkforcommandsresult'></a>Check for command's result

```bash
if ping -c 1 google.com; then
  echo "It appears you have a working internet connection"
fi
```

###  59. <a name='Grepcheck'></a>Grep check

```bash
if grep -q 'foo' ~/.bash_history; then
  echo "You appear to have typed 'foo' in the past"
fi
```

###  60. <a name='Alsosee'></a>Also see


* [Bash-hackers wiki](http://wiki.bash-hackers.org/) _(bash-hackers.org)_
* [Shell vars](http://wiki.bash-hackers.org/syntax/shellvars) _(bash-hackers.org)_
* [Learn bash in y minutes](https://learnxinyminutes.com/docs/bash/) _(learnxinyminutes.com)_
* [Bash Guide](http://mywiki.wooledge.org/BashGuide) _(mywiki.wooledge.org)_
* [ShellCheck](https://www.shellcheck.net/) _(shellcheck.net)_