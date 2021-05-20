Angular Setup:

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
  
    src: https://phoenixnap.com/kb/update-node-js-version




Component = Template(.html) + Class(.ts) + Metadata(decorators)

Component:
- If selector = 'app-student'
```language
  <app-student> </app-student>  
```
  
- If selector = ".app-student"

```language
<div class="app-student">

</div>
```

  - `<div class="app-student">` `</div>`  
- If selector = '[app-student]'
  - `<div app-student></div>`