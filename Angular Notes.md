## Angular Setup:

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


<br></br>

## Component:
- **Component = Template(.html) + Class(.ts) + Metadata(decorators)**

- If selector = 'app-student'
  ```language
  <app-student> </app-student>  
- If selector = ".app-student"
  ```language
  <div class="app-student">
  </div>
- If selector = '[app-student]'
  ```language
  <div app-student></div>`

## Data Binding

### Interpolation
 - This allows injection of dynamic strings into the HTML text. It’s syntax is {{…}} 
 - Binding data from class to the view
 - Using {{}}, we can retrieve the value
 - {{name.toUppercase}}
 - {{name.length}}
 - Cant be used for boolean values. Need to take help of property binding .
    ``` 
    <input type="text" [disabled]="flag" id="{{ courseID }}" value="Angular10" />

    ```
    <input type="text" bind-disabled="flag" id="{{ courseID }}" value="Angular10" />


### Property Binding
- Used for setting of a property value on a view element. It’s syntax is […]
- Html vs dom property?
  ```
    <input type="text" value="Angular10">
  
- `$0.getAttribute('value')`   -- HTML attribute

  `$0.value`   -- DOM values

    Even if the value changes in the text input, the html attribute will still be "Angular10" only whereas DOM value will be as per the input in the input box

  ![dom vs html](http://geoff-fox.com/wp-content/uploads/2017/03/attribute-binding.png)

