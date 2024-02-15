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


## Variables
