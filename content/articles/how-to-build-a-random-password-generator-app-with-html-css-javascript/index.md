A Password Generator is an application that can automatically generate passwords for you. These generated passwords consist of alphabets, numbers, and symbols. This application helps the user create a solid password that cannot be easily guessed or brute-forced.

In this article, you will learn how to build a random password generator application with HTML, CSS, and JavaScript.

The password generator application you will build will have a container where there would be an input field, a copy button that copies the password that has been randomly generated. You will create an input button that shows the user the preferred length they want for their password, a minimum of 5 words and a maximum of 20 words. It may include upper and lower case letters as well as symbols. It will also have a generate password button that outputs the random password. Below is a picture of how the application would look like.

![password generator app](/engineering-education/how-to-build-a-random-password-generator-app-with-HTML-CSS-javascript/password-generator-app.jpg)

### Prerequisites

You should have a fundamental knowledge of:

The reader should have a Fundamental knowledge of HTML, CSS and a basic understanding of JavaScript, including functions.

### Writing The Markup Of The Password Generator Application
You will start by opening any preferred text editor, then create an HTML file and save it with `index.html`. In there is where we would write the markup for the application. Now you are going to write out doctype HTML and the header like this below.

HTML
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>PASSWORD GENERATOR APP</title>
    <link rel="stylesheet" href="layout.css" />
    <script src="script.js" defer></script>
  </head>
</html>
```

Next is the `title` of our markup page, the CSS code for linking an external CSS file that you would save as `layout.css`, and the external javascript file you would also save as `script.js` then the closing `head` tag.

Now you will write the codes for the body of the application, which you will see in the code below.

HTML
```
<body>
  <form id="passwordGeneratorForm">
    <div class="container">
      <h2>Password Generator Application</h2>
      <div class="result__container">
      <span id="result"></span>
      <button id="copy">Copy</button>
    </div>
    <div class="options">
      <div class="option">
        <label>Length</label>
        <input type="number" id="length" min="4" max="20" value="10">
      </div>
      <div class="option">
        <label>Include Uppercase</label>
        <input type="checkbox" id="uppercase" checked>
      </div>
      <div class="option">
        <label>Include Numbers</label>
        <input type="checkbox" id="numbers" checked>
      </div>
      <div class="option">
        <label>Include Symbols</label>
        <input type="checkbox" id="symbols" checked>
      </div>
    </div>
    <button class="btn" id="generate" type="submit">Generate Password</button>
    </div>
  </form>
</body>
```

According to the codes above, you would start the random password generator application like a form inside the HTML body. Then, you will create a div `form ID` and name it password generator form. You will then create a class `container`.Inside this class, you have an `h2` tag where you will input “password generator application.” You need to create another div class for the result or container where you will create a `span ID`called “result,” which shows the result of the randomly generated password. Then, you can create a `button id` called “copy,” which will then eventually copy the password generated to our clipboard. The functionality of all the div classes will be made possible when you start implementing the javascript codes.

Now, you would be creating a class called `options`, and you are going to create another class of different options inside the initial div class `options` you created. You will need these options for the kind of random passwords the user wants. For instance, the length of the password, if the user wants it to be uppercase, or if the user wants to include numbers and symbols. You will also create another div and build a button with the id “generate,”  which will generate the random password.

### Styling The Application

We all know that CSS is what brings out the beauty of an application or website. It makes us able to structure the styles, layout, fonts, and properties. Now create a file and save it with “layout.css.” This is where you will write all the CSS for the application. Below are the CSS codes for the application

CSS
```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  font-family: 'Oswald', sans-serif;
  background-color: #39378f;
}

.container {
  padding: 1rem 1.5rem;
  border: 1px solid black;
  width: 350px;
  background-color: #4abd15;
}

h2 {
  text-align: center;
  padding: 15px 0;
}


.option {
  display: flex;
  justify-content: space-between;
  padding: 4px;
}
.result__container {
  height: 50px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid black;
  padding: 0 5px;
}

.result-container #result {
  word-wrap: break-word;
  max-width: calc(100% - 40px);
}

.result__container #copy {
  height: 40px;
  width: 40px;
  background-color: #eb1606;
  color: #ffffff;
  border: none;
  cursor: pointer;
  outline: none;
}

.result__container #copy:hover {
  background-color: #1c2541;
  color: #ffffff;
}

#generate {
  height: 40px;
  width: 100%;
  border-radius: 10px;
  border: none;
  background-color: #0b132b;
  color: #ffffff;
  font-size: 15px;
  font-weight: bold;
  cursor: pointer;
  outline: none;
}

#generate:hover {
  background-color: #5bc0be;
  color: #ffffff;
}
```

### Understanding The ASCII Character Table

First of all, I don’t advise you to jump straight to coding the JAVASCRIPT without a prior understanding of the ASCII character. The logic behind the random password generator is understanding ASCII. Below is a table of the ASCII character.

![ascii-table](ascii-table.jpg)

Source:[https://favpng.com/png_view/binary-code-ascii-character-encoding-value-png/sdHr9cAb](https://favpng.com/png_view/binary-code-ascii-character-encoding-value-png/sdHr9cAb)

The full meaning of ASCII is American Standard Code for Information Interchange, if you look at the uppercase ASCII A, it has a value of 65, and if you add the values with one, you will get all the 26 uppercase characters also the lowercase begins at the decimal 97 and keeps going up to 122, the symbols are at various places in the image above all we are going to do to use these decimal values to generate different passwords, I advice you to read more about ASCII if you still don’t understand

### Writing The Javascript

Start by linking the different HTML elements in the javascript using the code below:

JAVASCRIPT
```
// Getting the DOM Elements

const resultDOM = document.getElementById("result");
const copybtnDOM = document.getElementById("copy");
const lengthDOM = document.getElementById("length");
const uppercaseDOM = document.getElementById("uppercase");
const numbersDOM = document.getElementById("numbers");
const symbolsDOM = document.getElementById("symbols");
const generatebtn = document.getElementById("generate");
const form = document.getElementById("passwordGeneratorForm");
```


Next, you will work on the character codes you will use to form the randomly generated password. Below is the code to create character codes for the application. For the uppercase codes, you will pass the low of 65, which is the value of uppercase A and the high value of 90 also, the uppercase Z you can recall from the ASCII table. You will also do this for the lowercase characters and numbers. But generating the character codes for the symbols is different because they are allocated in the various places of the ASCII table. This will then make you use the `.concat function` to combine them into a single array. This function is a method in JavaScript which allows the concatenation of strings and arrays. For the symbols, they start at 33 and increase up to 47 and then continue at 58.

JAVASCRIPT
```
// Generating Character Codes For The Application
const UPPERCASE_CODES = arrayFromLowToHigh(65, 90);
const LOWERCASE_CODES = arrayFromLowToHigh(97, 122);
const NUMBER_CODES = arrayFromLowToHigh(48, 57);
const SYMBOL_CODES = arrayFromLowToHigh(33, 47)
  .concat(arrayFromLowToHigh(58, 64))
  .concat(arrayFromLowToHigh(91, 96))
  .concat(arrayFromLowToHigh(123, 126));
```

The next thing you want to do is build the `copy` button and copy to clipboard functionality. You can achieve this by creating a `textarea` element, sets its value to the value you want to copy, append the `textarea` to the HTML document, select the value by using the `select()` method, execute the `exeCommand(copy)` method and remove the `textarea`. Now you are going to start with a `copybtnDOM` button. We will listen to the click event on the “copybtnDOM” element to the function when the event is triggered. Meanwhile, inside that function, you will create a `textarea` element using the `createElement` method in javascript. Below are the codes for building that functionality, and I will explain every syntax.

JAVASCRIPT
```
// Copy Password Button

copybtnDOM.addEventListener("click", () => {
  const textarea = document.createElement("textarea");
  const passwordToCopy = resultDOM.innerText;
  // A Case when Password is Empty
  if (!passwordToCopy) return;
  // Copy Functionality
  textarea.value = passwordToCopy;
  document.body.appendChild(textarea);
  textarea.select();
  document.execCommand("copy");
  textarea.remove();
  alert("Password Copied to Clipboard");
});
```


In the above code for `const textarea=document.createElement(‘textarea’)`, you just created a variable that will store any value that has to be copied, and you can get the value using the `resultDOM.innerText` because the text inside the `resultDOM` holds your randomly generated password. Then, the `if (!passwordToCopy) return;` just means if the “passwordToCopy” variable is empty, it should just return the function. The `textarea. value = passwordToCopy;` syntax is used to set the “textarea” value with the value you want to copy.

Next is the `document.body.appendchild(textarea);` all you want to do here is append the text area value to the body of your document. The append child method adds a node to the end of the list of the children of a specified parent node. You need to select the elements you want to copy so you will use the `textarea. select();` method then to copy the elements, you will use the `document.execCommand(‘copy’);` method. This method executes the specified command for the selected part of an editable section which is the textarea. The `copy` command inside the function will copy the values of the editable section, after which you need to remove the “textarea” by using the `textarea.remove();`. This will give the user a notification that the password is successfully copied. After that, you will code a “simple alert” for it to show it, the `alert(‘password copied to clipboard’)` function. With all these written down, the application can not yet generate random passwords because you have not finished implementing the functionality that creates random passwords.
Also, if you click the button, you will observe that the page keeps reloading. You need to disable this reloading behavior by using a web API called `preventDefault`. This method will make sure the default behavior is not affecting the page. You can do this using the code below.

JAVASCRIPT
```
// Checking the options that are selected and setting the password
form.addEventListener("submit", (e) => {
  e.preventDefault();
  const characterAmount = lengthDOM.value;
  const includeUppercase = uppercaseDOM.checked;
  const includeNumbers = numbersDOM.checked;
  const includeSymbols = symbolsDOM.checked;
  const password = generatePassword(
    characterAmount,
    includeUppercase,
    includeNumbers,
    includeSymbols
  );
  resultDOM.innerText = password;
});
```


In the above code, the first step you take is to disable the default behavior using the function `e.preventDefalult();`. You are listening to the submit event. To get the event, you will pass it to a function using the arrow functions the “e” represents the event. After that, you will be checking the multiple options. In other words, you can access the values inside the password length field by using the `.value` getter method, which returns the input value, also the `.checked` getter, which returns true if the checkboxes are selected or not. Still, it will return false if the checkboxes are not selected. If you look at the codes correctly, you will see that the values you are getting from the options are stored inside separate variables. We are going to create a variable called `password`. This variable will store the value returned by the `generatePassword` function. The `generatePassword` function takes four arguments because you have only four options to select from and the values stored are the arguments by the variables you declared. Lastly, the `innerText` method would target the text inside `resultDOM` then change it with the generated password.

Okay, next is the password generating function, which is the most critical function in our application because it will create the password you are getting from this function. Before you build the function, remember the above codes. You will see that the `generatePassword` function takes only four arguments, so you need to pass the four arguments when creating this function. Everything is going to be shown in the codes below, including building the whole password generating function.

JAVASCRIPT
```
// The Password Generating Function
let generatePassword = (
  characterAmount,
  includeUppercase,
  includeNumbers,
  includeSymbols
) => {
  let charCodes = LOWERCASE_CODES;
  if (includeUppercase) charCodes = charCodes.concat(UPPERCASE_CODES);
  if (includeSymbols) charCodes = charCodes.concat(SYMBOL_CODES);
  if (includeNumbers) charCodes = charCodes.concat(NUMBER_CODES);
  const passwordCharacters = [];
  for (let i = 0; i < characterAmount; i++) {
    const characterCode =
      charCodes[Math.floor(Math.random() * charCodes.length)];
    passwordCharacters.push(String.fromCharCode(characterCode));
  }
  return passwordCharacters.join("");
};
```


Now let me explain the codes after passing the four arguments. You want the password to be lowercase if no option is checked. Inside the function, you will create a variable that will store an array of the character codes, and you will assign the lowercase character codes by using the `let charCodes`. After that, you need to check if the options are true or not by using the conditional statements `if (includeUppercase) charCodes` for uppercase code, `if (includeSymbols) charcodes` for symbol codes, and `if (includeNumbers) charcodes` for number codes. Now depending on the options selected, you concatenate the values to the `charCodes` variable. For the password that it will create, you will create an empty array and call it `passwordCharacters`. After that, you will create a loop that will loop until it reaches the number of characters you want. While inside the loop, you will generate random character codes from the available values in the `charCodes` array. And then convert the characters from the character codes and push them into the `passwordCharacters`array so that you have completed the `generatePasswordfunction`. Now you will loop till the character amount you are getting from the input field in the app. The `charCodes` variable has all the character codes. It all depends on the options the user selected. You will now generate a random index position of the array by using the ` math.random()` method, you multiply it with the `charCodes.length` to restrict it to generate numbers up to the highest index position. Next is the `Math.floor`, which will complete the number that is generated.

Lastly, the `String.fromCharCode(characterCode)` will generate the string from the character code, and the `passwordCharacters.push()` will push the character to the array, the `return passwordCharacters.join(“)` will convert the array to a string and return it.

All you need to do now is create a function that generates the decimal values of the characters, and in the end, you will convert all these values to characters using the method below.

JAVASCRIPT
```
This is an example
* Let array FromlowToHigh = (low, high) => {
Const array = [];
For (let i = low; i <= high; i++) {
 array.push(i);
}
Return array;
}; *
```


The function will take two inputs: the highest and the other for the lowest value. It just increments until the highest value is achieved. All the incremented values are pushed to an array, and the function then returns the array, all you are doing is generating the character code function. Here is the code below.

JAVASCRIPT
```
// Character Code Generating Function
function arrayFromLowToHigh(low, high) {
  const array = [];
  for (let i = low; i <= high; i++) {
    array.push(i);
  }
  return array;
}
```

Now, if you run the codes, our random password generator application would work perfectly well. We have successfully built our password generator application.

### Conclusion

There are many other ways to build a random password generator application. This tutorial is just one way to achieve it. You can also research different ways of creating it as long as it performs the same functionality. If you want the source codes for this application, you can get them from my Github repo [here](https://github.com/destiny251/random-password-generator-app-).