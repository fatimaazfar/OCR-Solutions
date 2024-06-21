# OCR Solutions

OCR Solutions is a comprehensive tool that combines multiple OCR (Optical Character Recognition) technologies to extract text from images. The project demonstrates how to utilize Tesseract OCR, EasyOCR, and Google Cloud Vision to convert images into readable and editable text.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Setup Google Cloud Vision API](#setup-google-cloud-vision-api)
- [Usage](#usage)
  - [Tesseract OCR](#tesseract-ocr)
  - [EasyOCR](#easyocr)
  - [Google Cloud Vision](#google-cloud-vision)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Multiple OCR Technologies**: Leverages Tesseract OCR, EasyOCR, and Google Cloud Vision for text extraction.
- **Easy Integration**: Simple and straightforward integration of each OCR tool.
- **Text Extraction**: Efficiently extracts text from images and saves it to a file.
- **Error Handling**: Robust error handling to manage exceptions and errors during OCR processing.

## Installation

To get started with OCR Solutions, follow these steps:

1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/OCR-Solutions.git
   cd OCR-Solutions
   ```

2. Install the required dependencies:
   ```sh
   pip install pytesseract Pillow easyocr google-cloud-vision
   ```

## Setup Google Cloud Vision API

To use Google Cloud Vision, you need to set up the API and get the credentials JSON file. Follow these steps:

1. **Create a Google Cloud Project**:
   - Go to the [Google Cloud Console](https://console.cloud.google.com/).
   - Click on the project drop-down and select **New Project**.
   - Enter a project name and click **Create**.

2. **Enable the Vision API**:
   - In the Google Cloud Console, navigate to **APIs & Services** > **Library**.
   - Search for "Vision API" and click on **Google Cloud Vision API**.
   - Click the **Enable** button.

3. **Set Up Service Account**:
   - Navigate to **APIs & Services** > **Credentials**.
   - Click on **Create Credentials** and select **Service Account**.
   - Enter a name and description for the service account and click **Create**.
   - In the **Role** dropdown, select **Project** > **Owner**, then click **Continue**.
   - Click **Done**.

4. **Create and Download the JSON Key**:
   - After creating the service account, click on it to open its details.
   - Go to the **Keys** tab and click **Add Key** > **Create New Key**.
   - Select **JSON** and click **Create**. This will download the JSON key file to your computer.
   - Rename the downloaded JSON file to `ocr-cloud-vision-424222-0778b1f83e3e.json` and place it in your project directory.

5. **Set the Environment Variable**:
   - Set the environment variable for the Google Cloud Vision API key:
     ```sh
     export GOOGLE_APPLICATION_CREDENTIALS="ocr-cloud-vision-424222-0778b1f83e3e.json"
     ```

## Usage

### Tesseract OCR

To extract text using Tesseract OCR:

1. Install Tesseract on your system:
   - On Windows: Download the installer from [here]([https://github.com/tesseract-ocr/tesseract/wiki](https://github.com/tesseract-ocr/tessdoc)).
   - On macOS: Use Homebrew: `brew install tesseract`.
   - On Linux: Use your package manager, e.g., `sudo apt-get install tesseract-ocr`.

2. Use the following code:

   ```python
   import pytesseract
   from PIL import Image

   def image_to_text(image_path):
       try:
           img = Image.open(image_path)
           text = pytesseract.image_to_string(img)
           return text
       except Exception as e:
           return str(e)

   if __name__ == "__main__":
       image_path = 'image.jpeg'
       extracted_text = image_to_text(image_path)
       print(extracted_text)
   ```

### EasyOCR

To extract text using EasyOCR:

1. Use the following code:

   ```python
   import easyocr

   def image_to_text(image_path):
       reader = easyocr.Reader(['en'])
       result = reader.readtext(image_path, detail=0)
       text = "\n".join(result)
       return text

   def save_text_to_file(text, file_path):
       with open(file_path, 'w') as file:
           file.write(text)

   if __name__ == "__main__":
       image_path = 'image.jpeg'
       output_file = 'output_easyocr.txt'
       raw_text = image_to_text(image_path)
       print("Raw text extracted from image:")
       print(raw_text)
       save_text_to_file(raw_text, output_file)
       print(f"\nRefined text saved to {output_file}")
   ```

### Google Cloud Vision

To extract text using Google Cloud Vision:

1. Use the following code:

   ```python
   import os
   from google.cloud import vision

   def image_to_text(image_path):
       client = vision.ImageAnnotatorClient()
       with open(image_path, 'rb') as image_file:
           content = image_file.read()
       image = vision.Image(content=content)
       response = client.text_detection(image=image)
       texts = response.text_annotations
       if texts:
           return texts[0].description
       else:
           return "No text detected"

   def save_text_to_file(text, file_path):
       with open(file_path, 'w') as file:
           file.write(text)

   if __name__ == "__main__":
       image_path = 'image6.jpeg'
       output_file = 'output6.txt'
       raw_text = image_to_text(image_path)
       print("Raw text extracted from image:")
       print(raw_text)
       save_text_to_file(raw_text, output_file)
       print(f"\nRefined text saved to {output_file}")
   ```

## Contributing

Contributions are welcome! Please fork this repository and submit a pull request for any enhancements or bug fixes.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the Apache 2.0 License. See `LICENSE` for more information.

---

Feel free to reach out if you have any questions or need further assistance with OCR Solutions!
