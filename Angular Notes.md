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
 - Cant be used for boolean values. Need to take help of PROPERTY BINDING .
    ``` 
    <input type="text" [disabled]="flag" id="{{ courseID }}" value="Angular10" />
    ```

  - Using Bind-disabled:
    ```
    <input type="text" bind-disabled="flag" id="{{ courseID }}" value="Angular10" />
    ``` 


### Property Binding
- Used for setting of a property value on a view element. It’s syntax is […]
- Html vs dom property?
  ```
    <input type="text" value="Angular10">
  
- `$0.getAttribute('value')`   -- HTML attribute

  `$0.value`   -- DOM values

    Even if the value changes in the text input, the html attribute will still be "Angular10" only whereas DOM value will be as per the input in the input box
  
- ### 1-way property binding
  ![1-way property binding](http://geoff-fox.com/wp-content/uploads/2017/03/property-binding.png)

- ### 1-way Attribute Binding
  ![1-way Attribute Binding](http://geoff-fox.com/wp-content/uploads/2017/03/attribute-binding.png)

- PROPERTY BINDING for boolean values
  ``` 
  <input type="text" [disabled]="flag" id="{{ courseID }}" value="Angular10" />
  ```

- Using Bind-disabled for boolean values:
  ```
  <input type="text" bind-disabled="flag" id="{{ courseID }}" value="Angular10" />
  ``` 


----------
### Class Binding
 - [class.TextBlue] = "flag"
 - class="TextBlue"
 - Apply multiple classes --> ngClass
  ```
     styles: [
    
      p {
        text-align: center;
        font-size: 30px;
        color: magenta;
      }

      .TextBlue {
        text-align: center;
        color: magenta;
      }
      .TextItalic {
        font-style: italic;
        color: red;
      }
      .TextColor {
        color: green;
      }
      .Underline {
        text-decoration: underline;
      }
     ]
```

In the class component
```
  public GroupOfStyles = {
    TextItalic: this.required,
    TextBlue: this.required,
    TextColor: this.required,
    Underline: this.required,
  };
```

In the view template - using ngClass,

`<h3 [ngClass]="GroupOfStyles">Class Binding 23322</h3>`

<br></br>
----------
### Style Binding
```
- **color directly**
  <h2 [style.color]="'yellow'">Hurrayyy Style Binding</h2>
- style through variable**
  <h2 [style.color]="myColor">Hurrayyy Style Binding</h2>
- styling through terinary operator 
  <h2 [style.color]="required ? 'grey' : myColor">Hurrayyy Style Binding</h2>
```