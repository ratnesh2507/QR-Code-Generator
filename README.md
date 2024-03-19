# QR Code Generator

## Features and Functionality

This Node.js script generates a QR code image based on a user-provided URL using the `inquirer`, `qr-image`, and `fs` modules. It prompts the user to input a URL, generates a QR code image for that URL, and saves both the image and the URL to separate files.

### Modules Used

- **inquirer:** Used for prompting the user to input the URL.
- **qr-image:** Used for generating the QR code image based on the URL.
- **fs:** Used for writing the QR code image and the URL to files.

### User Interaction

- The script prompts the user with a message to input a URL.
- The user inputs a URL, and the script proceeds to generate a QR code image and save it.

### QR Code Generation

- The user-provided URL is captured using `inquirer.prompt`.
- The `qr.image` function from the `qr-image` module generates a QR code image based on the URL.
- The generated QR code image is piped to a writable stream created using `fs.createWriteStream`, and it is saved as "qr_img.png".

### Saving the URL

- The user-provided URL is written to a text file named "URL.txt" using `fs.writeFile`.
- If an error occurs during file writing, it is handled using error handling.

### Error Handling

- The script handles errors that may occur during the execution of `inquirer.prompt` and file writing using `fs.writeFile`.
- Differentiates between errors related to rendering the prompt and other types of errors.

### Running the QR Code Generator

- Ensure you have Node.js installed on your system.
- Install the required modules (`inquirer`, `qr-image`) using npm or yarn.
- Execute the script using Node.js.
- Follow the on-screen prompt to input the URL.
- The QR code image and the URL will be saved to files.

### Sample Usage

```javascript
import inquirer from "inquirer";
import qr from "qr-image";
import fs from "fs";

inquirer
  .prompt([
    {
      message: "Type in your URL: ",
      name: "URL",
    },
  ])
  .then((answers) => {
    const url = answers.URL;
    var qr_svg = qr.image(url);
    qr_svg.pipe(fs.createWriteStream("qr_img.png"));

    fs.writeFile("URL.txt", url, (err) => {
      if (err) throw err;
      console.log("The file has been saved!");
    });
  })
  .catch((error) => {
    if (error.isTtyError) {
      // Prompt couldn't be rendered in the current environment
    } else {
      // Something else went wrong
    }
  });
