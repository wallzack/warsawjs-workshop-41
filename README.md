# warsawjs-workshop-41
WarsawJs Workshop#41 - JavaScript basics

## Into
- What is HTML?
- What is CSS?
- What is JavaScript?

## Where it starts
- What is navigation in browser?
- Why `index.html` is important?
- What is navigation and how it works?

## First steps
- What are html document main parts?
- How can i style elements on my site?
- Where i can put script in my page?

### Initial setup steps

1. Create empty file `index.html`
2. Fill basic `html` document with `head` and `body` with sample `hello world from html` text
    - define `doctype` with value `html`
    - define `html` document with empty `head` and `body`. Set lang attribute to `en`
    - define `head` content
        - add `meta` tag with attribute `charset` with value `utf-8` to set page encoding
        - add `title` tag with children equal to Your page title
3. Inside `body` add `div` with text `Test!`
4. Open file in browser to see if it works. Page should be blank, but title of window in Tab should be as You defined in `title` tag

## Linking style sheet and scripts

1. In `head` inside document, add new tag `link` with 3 attributes
    - `rel` attribute set linking relation, set value to `stylesheet`
    - `type` attribute with value `text/css`
    - `href` attribute with file name to link with value `styles.css`
2. Create empty file called `styles.css`
    - Add styling for `body`. You can create style rule with template below:
        ```text
          [tagName or selector]: {
              [cssProperty]: value;
          }       
        ```
    - Set rule `family-font` with value `sans-serif`
    - Check browser to see if stylesheet is loaded. Font should be changed.
3. Add empty `script` tag with 2 attributes:
    - `type` with value `text/javascript` so browser can parse text as javascript
    - `src` with value `game.js`
    - Open browser and inside devTools open network tab to see that browsers tries to download missing file
4. Create empty file `game.js`
    - inside add following line:
        `console.log('game script loaded');`
    - check browser console in devTools to see if message is printed
    
## Manipulating DOM

1. Add `id` attribute with value `gameContent` to `div` inside `body` to be able to find this element easlily in javascript code
2. Inside `game.js`:
    - Using built-in function `document.getElementById` find `div` with id `gameContent`
        - `document.getElementById` function takes one parameter - element id
        - store returned value using `const` for later usage.
    - Clear element content by changing element attribute `textConent` to empty string `''`
        - To access element attribute use dot operator `gameContent.textContent` and attribute name.
        - To change attribute value, just assign new value directly as so:
            - `element.attribute = newValue;`
    - Check browser to see that text initially loaded with html file is cleared
3. Create header element with text `Welcome to Hangman!`
    - To create element use `document.createElement`
        - Pass one argument to function with tagName with value `h1`
        - Set `textContent` attribute with value `Welcome to Hangman!`
    - Append created header element to previously stored found element
        - To append children to element use method `appendChild`
            - `element.appendChild(childElement);`
    - Check browser to see changes. Investigate Element tab in devTools to see html structure

## Listing for elements events

1. Create `div` element with text `Enter your name:`
    - store reference using `const`
2. Create `input` element
3. Add event listener to `input` element
    - to add event listener to element use element method `addEventListener`
        - first argument of this method is event name, listen for an user input event which value is `input`
        - second argument is function which will be called every times element fires proper event
        - inside event listener function add call to `console.log` and print value of event target
            - event listener function first argument is event object which describes event that took place
            - example:
            ```javascript
              nameInput.addEventListener('input', event => {
                   console.log(event.target.value)
              });
            ``` 
4. Append new elements to `div` with game content
5. Try entering some text and see if console is printing text entered in input

## Storing mutable value with `let`

1. Create variable for storing value from input
    - to store mutable value use `let`
    - while defining, assign empty string: `''`
    - `let` value can be reassigned while `const` not
2. Inside input event listener assign value from event to created variable
3. After assigning print value of created variable, instead directly reading from event

## Defining own functions

1. Create function called `welcomeView`, that takes no arguments
    - To create function use key word `function` followed by function name and than round parenthesis
    - example:
        ```javascript
          function nameIt() {
            // instructions
          }
        ```
2. Move logic to function
    - creating header
    - input code
3. Call function after defining 
    - check browser, there should be no visible changes
    
## Abstracting rendering

1. Create mutable variable for storing active view name
    - initialize variable with value `welcome`
2. Create function called `render` with no arguments
3. Inside `render` function clear game content
4. Inside `render` check which view render
    - use `if` with `else if` and `else` statement
        - example `if` statement:
        ```javascript
        if (condition1) {
          // do something
        } else if (condition2) {
          // do something else
        } else {
          // if all conditions are false
          // do something
        }
        ```
    - create case for value `welcome`
        - call `welcomeView` function
    - create default fallback
        - call `welcomeView` function
5. Check browser if there is still no changes in application visually

## Changing view

1. Inside `welcomeView` create button with text `Play game!`
2. Add event listener for event `click`
    - on every click change value of `activeView` to `play`
    - call `render` function
3. Create function `playView`
    - inside create `h1` element with text equal to `'Hi, ' + name`
4. Add new case inside `render` function for value `play`
    - call `playView` function
4. Check browser, test if clicking in button with text `Play game!` changes view

## Views loop

1. Inside `playView` create button with text `Finish`
    - listen for `click` event
        - change `activeView` value to `endGame`
        - call `render` function
2. Append button to game content
3. Create function `endGameView` with no arguments
    - create element `h1` with text `Game finished!`
    - create `button` element with text `Play again`
        - add event listener for `click` event
            - change active view to welcome view
            - call `render`
            
## Storing game state using object

1. Create object named `gameState`
    - example:
    ```javascript
    const objectName = {
       key1: 'value',
       key2: 123,
    }
    ```
2. Add field `name` with initial value `''`
3. Add field `activeView` with initial value `welcome`
4. Change all usage of `name` and `activeView` variables to use `gameState` object
5. Delete unused variables
5. Check browser to see if everything works

## SPA like updating content

1. At the begging of every view create empty `div`
2. Append all element to created `div` instead of global `gameContent` variable holding referance to root element
3. At the of of every function return `div` created at the begining
4. Create function `stateUpdate` with body below:
    ```javascript
    function stateUpdate(newGameState) {
      Object.assign(gameState, newGameState);
      render();
    }
    ```
5. Add 2 arguments to all views functions
    - first argument named `state`
    - second argument named `stateUpdate`
6. Pass `gameState` and `stateUpdate` to every view call
7. Change `gameState` usage inside views to `state`
8. Change lines modifiyng `gameState` with call to `stateUpdate`
9. Check browser to see that input wont change value - everything else should work as previoulsy

## Restoring input focus and cursor position

1. Inside `welcomeView`, after creating input element add call to `setTimeout` global function
2. Set input value using `state.name`
3. Focus element using `focus` method on element
4. Move cursor to end of the text by setting `selectionStart` attribute of input
5. Check input behaviuur in brwoser

## Selecting letters - arrays

1. At the begininng of file create variable to store all alphabet letters using array
    - example array syntax
    ```javascript
    const array = ['element1', 'element2'];
    ```
   - use english alphabet
2. Add to `gameState` object new field `selectedLetters`, and initialize it with empty array
3. Inside `playView` create `div` element for storing letters buttons
4. Iterate over all letters and create `button` element
    - set button text to equal iterated letter
    - set `disabled` attribute by checking in `state.selectedLetters` includes iterated letter
        - use array method `includes` which takes one argument - element in array you are looking for
    - add event listener for click event for every letter button
        - on click, update state so `state.selectedLetters` includes clicked letter
            - use array method `concat`
    - append button to buttons container
5. Append buttons container to view content

## Phrases - logic operators, randomness

1. Create array for holding phrases that user will be guessing
2. Create function for getting random phrase
    - create variable for holding random phrases array index
        - Use `Math.floor` and `Math.random` and phrases array length
        - return phrase at found index
3. Add new field to game state called `sectetPhrase` with initial value empty string
4. Inside `welcomeView` and button click listener update state so sectetPhrase inside game state will be random phrase
    - call previously created function 
5. Inside `playView` create container for phrase letters (`div`)
6. Split `state.secretPhrase` into array holding single letter
    - use string method `split(seperator)`
    - split by empty string
7. Iterate over every letter
    - create span element
    - check if letter is visible
        - is it visible if letter is space character
        - is it visible it letter is included in `state.selectedLetters`
        - use OR operator `||`
8. Set element text using previously calculated value (is letter visible) and ternary expression
    - example ternary expression:
    ```text
    condition ? ifConditionTrue : ifConditionFalse
    ```
   - use asterisk character `*`  for hidden letters
9. Append span to letters container
10. Append letters container to view before buttons container

## Detecting game end - unary operator and string template

1. Inside play view add mutable variable for storing count of visible letters
    - initialize it with number `0`
2. While iterating over phrase letters
    - use `if` statement to check if letter is visible and if it is - increase count of visible letters
        - use unary operator `number++`
3. After iterating all letters check if visible letters count is equal to secret phrases length
    - if condition is true, update state
        - set active view to `endGame`
        - set `selectedLetters` back to empty array  
4. Add to game state new field `mistakes` and initialize it with number `0`
5. Inside letter button listener check if clicked letter was mistake
    - use string method `indludes`
        - example
        ```javascript
        'abc'.includes('a'); // -> true
        ```
  - store check result in variable
6. Increase mistakes count if letter button was mistake
    - use ternary expression
    - for good click don't change value
7. In end view create `h3` element
    - use string template to iterpolate message for user, containg inforation about mistakes count
    - example string template
    ```javascript
    const foo = 123;
    const text = `count: ${foo}`;
    ```
   
## Persisting game state - localStorage, JSON api

1. Create variable for persisted game state from local storage
    - initialize it with loaded item from local storage
    - example
    ```javascript
    const storedValue = localStorage.getItem('key');
    ```
2. While initializing game state variable check if loaded game state from local storage is not empty and use this value to initialize game state
    - use ternary expression while assigning value
    - parse value using JSON api
        - use `parse` method from api to parse string into object
3. Update `stateUpdate` function so it updates local storage on every state update
    - use `setItem` method from local storage api
    - parse game state object to string using JSON api
        - use `stringify` method 
        
## Split code into separate file using global scope - closures

1. Create separate files for views functions
2. Add scripts in `index.html`
    - add before `game.js`
3. Move code to files
        
## Hosting site on github pages

1. Go push changes to github
2. Go to project settings
3. Scroll down to `GitHub Pages` section
4. Choose `master` branch as source
5. Done! Go to `username.gitbub.io/project-name`
  
## Splitting styles and scripts to separate file
- How to link external style sheet (css)?
- How to link external or local script from another file?
- What is JavaScript module? And how to link multiple JS files?

## Loading data
- How to load data on client side from static files?
- How to load data on client side from api?
- What is application state and do i need one?

## Creating template for dynamic HTML content
- What is template tag?
- Using template to dynamically show content

## [Extra] Hosting static page on GitHub Pages
- What is gh-pages?
- How can i use it?

## [Extra] Server side vs client side
- What is server side?
- What is client side?
- Where the work is done?





## Dictionary
- Tag/TagName - html element name, for example `div`
- Element/node - using proper tags You can create elements for example `<div>hello</div>`
- Attribute or element attribute - element can have additional attributes, for example: `charset` is attribute of `meta` tag - `<meta charset="utf-8">`
- Children of element/node are descent of this element, for example: `<div><p>hello</p></div>`, element with tag `p` is children of element with tag `div`
