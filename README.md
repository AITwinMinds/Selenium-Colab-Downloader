

# 🚀 Selenium-Colab File Downloader

## Overview
Selenium-Colab File Downloader is an automated Selenium-based script designed to simplify file downloads from websites requiring login credentials, specifically optimized for Google Colab environments.

## Features
- Automated login process
- Headless Chrome browser support
- Direct downloads to Google Drive
- Secure credential handling
- Configurable download settings

## Prerequisites
- Google Colab
- Selenium WebDriver
- Google Drive access

## Usage

### 1. Install Dependencies
```bash
!pip install selenium
!apt update
!apt install chromium-chromedriver
```

### 2. Mount Google Drive
```python
from google.colab import drive
drive.mount('/content/gdrive')
```

### 3. Dependencies and Imports
```python

# Import required libraries
from google.colab import drive
import time
import sys
import os
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from selenium import webdriver
from selenium.webdriver.common.by import By
```
**Explanation:**
- `selenium`: Web automation framework
- `google.colab.drive`: Mount Google Drive for file storage
- `time`: Add delays for page loading
- `webdriver`: Selenium's core automation class
- `By`: Locate web elements by different attributes

### 4. Chrome Options Configuration
```python
# Configure Chrome options for headless execution
options = webdriver.ChromeOptions()
options.add_argument('--headless')  # Run browser without visible UI
options.add_argument('--no-sandbox')  # Bypass OS security model
options.add_argument('--disable-dev-shm-usage')  # Overcome resource limitations

# Download preferences
prefs = {
    "download.default_directory": "/content/gdrive/MyDrive",  # Set download location
    "download.prompt_for_download": False,  # Disable download prompts
    "download.directory_upgrade": True,  # Enable directory upgrades
    "safebrowsing.enabled": True  # Enable safe browsing
}
options.add_experimental_option("prefs", prefs)  # Apply download preferences
```
**Key Points:**
- `headless`: Runs Chrome without visible interface
- `no-sandbox`: Bypasses security for Colab
- `disable-dev-shm-usage`: Resolves resource constraints
- Download preferences set to automatic, direct-to-Drive download

### 5. WebDriver Initialization
```python
# Initialize Chrome WebDriver with configured options
driver = webdriver.Chrome(options=options)
```
Creates a Chrome browser instance with predefined settings

### 6. Login Process
```python
# Navigate to login page
login_url = input("Enter the login page URL: ")
driver.get(login_url)
time.sleep(5)  # Wait for page to load

# Collect login credentials
email = input("Enter your email: ")
password = input("Enter your password: ")

# Find and interact with login form elements
email_input = driver.find_element(By.NAME, "email")
email_input.send_keys(email)

password_input = driver.find_element(By.NAME, "password")
password_input.send_keys(password)

# Locate and click login button
login_button = driver.find_element(By.CLASS_NAME, "ui.fluid.large.labeled.icon.primary.button")
login_button.click()

# Wait for login to complete
time.sleep(5)
```
**Login Automation Steps:**
1. Navigate to login URL
2. Locate email and password input fields
3. Enter credentials
4. Click login button
5. Wait for authentication

### 7. Download Process
```python
# Navigate to download page
download_url = input("Enter the file download URL: ")
driver.get(download_url)

# Extended wait time for download completion
time.sleep(800)  # Adjust based on file size/network speed

# Close browser
driver.quit()
```
**Download Steps:**
1. Navigate to download URL
2. Wait for download to complete
3. Close browser session
  
## Security Considerations
- Avoid hardcoding credentials
- Use secure input methods

## Limitations
- Requires manual URL and credential input
- Depends on website's specific HTML structure
- Limited to websites with standard login forms

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss proposed modifications.

## License
[MIT](https://choosealicense.com/licenses/mit/)
