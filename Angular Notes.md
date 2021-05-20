Hello World App


Latest version setup:
- Java setup
  - Open the terminal and run the below command.
    - `$ vim .bash_profile`
    - `export JAVA_HOME=$(/usr/libexec/java_home)`
  - save and exit from vim editor, then run the source command on .bash_profile
    - `$ source .bash_profile`
    - `$ echo $JAVA_HOME`

- Checking Node version
    `$ node --version`
  - Updateign the node verison
     - `npm cache clean -f`
     - `npm install -g n`
     - `n stable`