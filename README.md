# Testing Instructions Generator

The Testing Instructions Generator is a web-based tool designed to generate detailed testing instructions for a series of screenshots of an app. By providing optional context and uploading multiple screenshots, this tool creates structured testing cases that include descriptions, pre-conditions, testing steps, and expected results. It leverages a backend API that integrates with the Llava model to produce these instructions.

## Features

- Accepts multiple screenshots of an app in the order they appear.
- Allows optional context input to provide additional information for the test case generation.
- Automatically generates a collage of screenshots to be analyzed.
- Calls the Llava API to generate comprehensive testing instructions.
- Displays generated instructions in a readable format.

## Technologies Used

- **Frontend:** HTML, CSS, JavaScript
- **Backend:** Python, Flask
- **Image Processing:** PIL (Pillow)
- **API Integration:** Requests library
- **AI Model:** Llava Model API (Ollama)

## Prompting Strategy
The prompting strategy used in this tool involves a carefully constructed prompt that provides the AI model with both visual and contextual information. The generated prompt sent to the Llava API includes:
- **Context Provided by the User:** If the user has added any optional context, it is included in the prompt to provide additional background information for generating relevant test cases.
- **Description of the Collage of Screenshots:** The tool converts multiple screenshots into a single collage image, which is sent to the AI model. This is done as sending multiple images results in the size of payload becoming too large (as images need to be encoded to base64 to send to the api), causing the request to fail. The prompt specifies that the collage contains a sequence of app screenshots, and it instructs the AI to generate detailed testing instructions for this collage.
- **Structured Request for Testing Instructions:** The prompt requests a structured output that includes:
  - **Description:** A brief description of the test case scenario.
  - **Pre-Conditions:** Conditions that must be met before the test can be executed.
  - **Testing Steps:** Step-by-step actions the tester should perform.
  - **Expected Results:** What the tester should observe if the app behaves correctly.

## API Integration
The tool interacts with the Llava API through a backend written in Python (Flask). The API call is responsible for generating detailed test cases using the Llava model.

### Endpoint
- **POST** `/generate-instructions`
- Accepts `context` as a form field.
- Accepts `screenshots` as a list of files.
- Returns generated testing instructions or an error message.
