# Bash_Scripting_Cheatsheet


## Basics

1. Bash scripts always start with a shebang (#!) + the shell used to interpret the script (bash, sh, ...)
   ```
   #!/bin/bash
   ```

2. Scripts are sourced by either:
   ```
   bash test.sh
   ```
   ```
   ./test.sh
   ```

3. Scripts are text files that have execute permissions. Make sure to adjust its permissions to be able to execute it.
   ```
   chmod 755 test.sh
   ```

4. Script extension does not matter. But, it is advisable to name scripts with the extension `.sh` to make it easily recognizable---**IT IS THE LAW!**


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
