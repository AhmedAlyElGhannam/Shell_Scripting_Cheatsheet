# Shell_Scripting_Cheatsheet


## Basics

1. Shell scripts always start with a shebang `#!` + the shell used to interpret the script (bash, sh, ...)
   ```
   #!/bin/bash
   ```

1. Scripts are sourced by either:
   ```
   bash test.sh
   ```
   ```
   ./test.sh
   ```

1. Scripts are text files that have execute permissions. Make sure to adjust its permissions to be able to execute it.
   ```
   chmod 755 test.sh
   ```

1. Script extension does not matter. But, it is advisable to name scripts with the extension `.sh` to make it easily recognizable---**IT IS THE LAW!**

1. Comments are written by writing a `#` sign before text.

## Variables _(NO SPACES BEFORE OR AFTER =)_

1. Variables that store numbers and strings---with no spaces---are defined as:
   ```
   nice=69
   ```

1. Variables are used in commands by writing `$` before their name.
   ```
   echo $nice
   ```

1. Variables that store a space-separated string are defined between single quotes.
   ```
   nice='hi bois'
   ```

1. Variables that store stuff between double quotes indicate that there is a substitutable element inside---i.e.; another variable whose value will be replaced inside this string variable.
   ```
   nice=69

   niceness="$nice is nice"
   ```

1. To save a command as a variable, use `$(COMMAND)`.
   ```
   myvar=$( ls /etc | wc -l )
   ```

1. To export a variable to a child process---a variable available in script1 will be copied to script2---inside script1:
   ```
   .
   .
   .
   export var1
   ./script2.sh
   ```
   
1. Special variables:
   1. $0 - The name of the Bash script.
   1. $1 - $9 - The first 9 arguments to the Bash script. (As mentioned above.)
   1. $# - How many arguments were passed to the Bash script.
   1. $@ - All the arguments supplied to the Bash script.
   1. $? - The exit status of the most recently run process.
   1. $$ - The process ID of the current script.
   1. $USER - The username of the user running the script.
   1. $HOSTNAME - The hostname of the machine the script is running on.
   1. $SECONDS - The number of seconds since the script was started.
   1. $RANDOM - Returns a different random number each time is it referred to.
   1. $LINENO - Returns the current line number in the Bash script.
  

## User Input

1. Multiple variables can be read and stored using `read` command inside a script:
   ```
   read nice69 nice420 nice69420
   ```

1. User can be prompted to enter a value by a message using `-p` or `-sp` flags with `read`. `-p` gives a message to the user _and_ echos their input in terminal, `-sp` gives a message to the user _but does not_ echo their input in terminal---makes it hidden like passwords.
   ```
   read -p 'Enter Username: ' name
   read -sp 'Enter Password: ' pass
   ```


## Arithmetic Operations

1. The keyword `let`---kinda like Rust---stores the result of an arithmetic operation inside a variable. All the forms below are valid.
   ```
   let hehe=60+9
   let "hehe = 60 + 9"
   let hehe++
   let "hehe = $nice - 9 + 9"
   ```

1. Operators and their corresponding operation are:
   1. +, -, \*, /	--> addition, subtraction, multiply, divide
   1. var++	--> Increase the variable var by 1
   1. var--	--> Decrease the variable var by 1
   1. %	--> Modulus (Return the remainder after division)
  
1. The keyword `expr` returns the result of an aritmetic operation and **does not store it.** Beware that there must be space to separate expression elements.
   ```
   expr 50 + 19
   ```

1. A better and more versatile way to write and/or use aritmetic expressions is y writing them in `$((EXPR))`. This way, variables are substituted automatically without needing `$` before is, no need to nitpick over spaces before and after expressions, and expression can be either returned directly like `expr` or stored inside a variable like `let`. There is also **no need** to write `\` before `*` to perform multiplication.
   ```
   a=$(( 4 + 5 ))
   a=$((3+5))
   b=$(( a + 3 ))
   b=$(( $a + 4 ))
   (( b++ ))
   (( b += 3 ))
   a=$(( 4 * 5 ))
   ```

1. Although it is not an arithmetic operation, finding the length of a variable is sometimes useful. It is done by `${#VAR}`.
   ```
   hehe='Hello, bois'
   echo ${#hehe} # 11
   ```


## If Statements

1. If statement syntax is as shown. Note that the condition you are testing is written between square brackets. Notice that `if` is ended by `fi`; this is a common occurance in shell scripting syntax.
   ```
   if [ <some test> ]
   then
      <commands>
   fi
   ```

1. The following operators can be used in the `[ <test> ]` line. Note that the `[ ]` is a reference to the command `test` which can be used to test the expression before writing it in an if statement.
   1. ! EXPRESSION --> The EXPRESSION is false.
   1. -n STRING --> The length of STRING is greater than zero.
   1. -z STRING --> The lengh of STRING is zero---i.e.; it is an empty string.
   1. STRING1 = STRING2 --> STRING1 is equal to STRING2 _as a string in terms of elements and their lengths_
   1. STRING1 != STRING2 --> STRING1 is not equal to STRING2 _as a string in terms of elements and their lengths_
   1. INTEGER1 -eq INTEGER2 --> INTEGER1 is _numerically_ equal to INTEGER2
   1. INTEGER1 -gt INTEGER2 --> INTEGER1 is _numerically_ greater than INTEGER2
   1. INTEGER1 -lt INTEGER2 --> INTEGER1 is _numerically_ less than INTEGER2
   1. -d FILE --> FILE exists and is a directory.
   1. -e FILE --> FILE exists.
   1. -r FILE --> FILE exists and the read permission is granted.
   1. -s FILE --> FILE exists and it's size is greater than zero (ie. it is not empty).
   1. -w FILE --> FILE exists and the write permission is granted.
   1. -x FILE --> FILE exists and the execute permission is granted.
  
1. If-else statement syntax is written as:
   ```
   if [ <some test> ]
   then
      <commands>
   else
      <other commands>
   fi
   ```

1. If-else-if statement is written as:
   ```
   if [ <some test> ]
   then
      <commands>   
   elif [ <some test> ]
   then
      <different commands>
   else
      <other commands>
   fi
   ```

1. Boolean expressions---such as `||` and `&&`---can be used to make a compound test for an if statement:
   ```
   if [ -r $1 ] && [ -s $1 ]
   then
   .
   .
   .
   ```

