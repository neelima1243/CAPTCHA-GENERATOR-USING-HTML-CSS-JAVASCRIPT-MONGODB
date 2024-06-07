# CAPTCHA Generator
## Overview
Description
The CAPTCHA Generator project is a versatile and robust solution designed to enhance the security of web applications by distinguishing between human users and automated scripts (bots). Built using HTML, CSS, and JavaScript, this CAPTCHA generator creates dynamic images with randomized text that users must correctly identify and enter. The primary goal is to prevent automated systems from performing actions such as submitting forms, creating accounts, and posting content, thereby protecting your application from spam and abuse.
This project is a CAPTCHA generator, designed to create images containing randomized text that can be used to differentiate between human users and automated scripts (bots). The project includes features for generating CAPTCHA images, customizing the text and appearance, and validating user responses.

 **Validate CAPTCHA:**

    Users can enter the text they see in the CAPTCHA image into the input field and submit it. The CAPTCHA validation logic will check the input against the generated CAPTCHA text and display a success or failure message.

## Customization

You can customize the appearance and behavior of the CAPTCHA by modifying the HTML, CSS, and JavaScript files.

### HTML

The structure of the CAPTCHA generator is defined in `captcha.html`:
```html
<html lang="en">
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Captcha Generator</title>
    <h1>CAPTCHA GENERATOR</h1>
    <!-- Font Awesome Icons -->
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css"
    />
    <!-- Google Fonts -->
    <link
      href="https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@500&display=swap"
      rel="stylesheet"
    />
    <!-- Stylesheet -->
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="container">
     <h1>CAPTCHA GENERATOR</h1>
      <div class="wrapper">
        <canvas id="canvas" width="200" height="70"></canvas>
        <button id="reload-button">
          <i class="fa-solid fa-arrow-rotate-right"></i>
        </button>
      </div>
      <input
        type="text"
        id="user-input"
        placeholder="Enter the captcha....."
      />
      <button id="submit-button">Submit</button>
    </div>
    <!-- Script -->
    <script src="script.js"></script>
  </body>
</html>


####CSS
The styling of the CAPTCHA generator is defined in 'style.css':
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    text-align: center;
  }
  body {
    height: 100vh;
    background-image:url("https://t4.ftcdn.net/jpg/05/75/84/99/240_F_575849931_j0h5pEWF8XMd9OhGZhbODPL1ELaMQR75.jpg");
  }
  .container {
    width: 32em;
    background-color: #ffffff;
    padding: 5em;
    border-radius: 0.6em;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    box-shadow: 0 1em 2em rgba(0, 0, 0, 0.25);
  }
  .wrapper {
    display: flex;
    align-content: center;
    justify-content: space-between;
    margin: 1em 0;
  }
  canvas {
    border: 1px solid #000000;
    border-radius: 0.4em;
  }
  button#reload-button {
    font-size: 26px;
    width: 4.6em;
    background-color: #b3398a;
    border: none;
    border-radius: 0.4em;
    color: #ffffff;
  }
  input[type="text"] {
    font-family: "Roboto Mono", monospace;
    font-size: 1.05em;
    width: 100%;
    padding: 1em 0.7em;
    border: 1px solid #000000;
    border-radius: 0.4em;
  }
  button#submit-button {
    width: 100%;
    background-image:url("https://t4.ftcdn.net/jpg/05/71/81/85/240_F_571818551_ZSKAUfkPMzHJKXQUIGJPyRqQ2wi20UG7.jpg");
    color: #ffffff;
    font-size: 1.5em;
    border: none;
    margin-top: 1em;
    padding: 0.8em 0;
    border-radius: 0.4em;
    font-family: "Roboto Mono", monospace;
  }

 #####JavaScript
The CAPTCHA generation and validation logic is defined in 'script.js':

//Initial References
let submitButton = document.getElementById("submit-button");
let userInput = document.getElementById("user-input");
let canvas = document.getElementById("canvas");
let reloadButton = document.getElementById("reload-button");
let text = "";

//Generate Text
const textGenerator = () => {
  let generatedText = "";
  /* String.fromCharCode gives ASCII value from a given number */
  // total 9 letters hence loop of 3
  for (let i = 0; i < 3; i++) {
    //65-90 numbers are capital letters
    generatedText += String.fromCharCode(randomNumber(65, 90));
    //97-122 are small letters
    generatedText += String.fromCharCode(randomNumber(97, 122));
    //48-57 are numbers from 0-9
    generatedText += String.fromCharCode(randomNumber(48, 57));
  }
  return generatedText;
};

//Generate random numbers between a given range
const randomNumber = (min, max) =>
  Math.floor(Math.random() * (max - min + 1) + min);

//Canvas part
function drawStringOnCanvas(string) {
  //The getContext() function returns the drawing context that has all the drawing properties and functions needed to draw on canvas
  let ctx = canvas.getContext("2d");
  //clear canvas
  ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);
  //array of text color
  const textColors = ["rgb(0,0,0)", "rgb(130,130,130)"];
  //space between letters
  const letterSpace = 150 / string.length;
  //loop through string
  for (let i = 0; i < string.length; i++) {
    //Define initial space on X axis
    const xInitialSpace = 25;
    //Set font for canvas element
    ctx.font = "20px Roboto Mono";
    //set text color
    ctx.fillStyle = textColors[randomNumber(0, 1)];
    ctx.fillText(
      string[i],
      xInitialSpace + i * letterSpace,
      randomNumber(25, 40),
      100
    );
  }
}

//Initial Function
function triggerFunction() {
  //clear Input
  userInput.value = "";
  text = textGenerator();
  console.log(text);
  //Randomize the text so that everytime the position of numbers and small letters is random
  text = [...text].sort(() => Math.random() - 0.5).join("");
  drawStringOnCanvas(text);
}

//call triggerFunction for reload button
reloadButton.addEventListener("click", triggerFunction);

//call triggerFunction when page loads
window.onload = () => triggerFunction();

//When user clicks on submit
submitButton.addEventListener("click", () => {
  //check if user input  == generated text
  if (userInput.value === text) {
    alert("Success");
  } else {
    alert("Incorrect");
    triggerFunction();
  }
});


Key Features:
1.Random CAPTCHA Text Generation:
         Produces unique alphanumeric strings for each CAPTCHA instance, ensuring unpredictability.
2.Customizable Appearance:
         Offers flexibility in modifying fonts, sizes, colors, and styles to match your application's design.
3.Canvas-based Rendering:
         Utilizes HTML5 canvas for creating CAPTCHA images, allowing for intricate designs and effects.
4.Noise and Distortion:
         Enhances security by adding visual noise and distortions, making it challenging for bots to decipher the text.
5.User Interaction:
         Provides a refresh button for users to generate a new CAPTCHA if the current one is difficult to read.
6.Lightweight and Fast:
         No external dependencies required, ensuring quick load times and easy integration.
7.Responsive Design:
         Adapts to various screen sizes, ensuring usability on both desktop and mobile devices.
8.Accessible and Configurable:
         Adjust difficulty and security levels based on user needs, ensuring a balance between user-friendliness and protection.

Practical Uses:

*Form Security: Protects sign-up, login, and contact forms from automated submissions.

*E-commerce: Secures order forms and checkout processes to prevent fraudulent activities.

*Content Integrity: Reduces spam in comments, reviews, and feedback sections.

*Polls and Surveys: Ensures the accuracy of responses by preventing bot participation.

*Online Contests: Maintains fairness by restricting entries to real users.

                                        The CAPTCHA Generator is an open-source project, encouraging contributions and enhancements from the community. By integrating this CAPTCHA generator into your web application, you can significantly improve security, reduce spam, and ensure a better user experience.

