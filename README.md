# CAPTCHA Generator
## Overview

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


CSS
The styling of the CAPTCHA generator is defined in styles.css:
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

JavaScript
The CAPTCHA generation and validation logic is defined in script.js:



