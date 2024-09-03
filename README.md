# How to Bypass CAPTCHA With Playwright

This step-by-step tutorial demonstrates how to use Playwright to bypass CAPTCHA challenges using Python. The tutorial will also discuss the perks of using Oxylabs’ Web Unblocker instead of the `playwright-stealth` library. 

### 1. Install dependencies
Install the Playwright library and the stealth package.

```pip install playwright playwright-stealth```

### 2. Import modules 
Use the synchronous version of the Playwright library for a straightforward and linear program flow.

```
from playwright.sync_api import sync_playwright
from playwright_stealth import stealth_sync
```

### 3. Create a headless browser instance
Define the `capture_screenshot()` function that encapsulates the whole code to open a headless browser instance, visit the url, and capture the screenshot. In this function, create a new `sync_playwright` instance and then use it to launch the Chromium browser in headless mode.

```
# Define the function to capture the screenshot
def capture_screenshot():
    # Create a playwright instance
    with sync_playwright() as play_wright:
        browser = play_wright.chromium.launch(headless=True)

        # Create a new context and page
        context = browser.new_context()
        page = context.new_page()
```

### 4. Apply the stealth settings
After creating the browser context, enable Playwright CAPTCHA bypasses by applying the stealth settings to the page using the `playwright-stealth` package. Stealth settings help in reducing the chances of automated access detection by hiding the browsers’ automated behavior.

```
        # Apply the stealth settings
        stealth_sync(page)
```

5. Navigate to the page
In the next step, navigate to the target URL by specifying your required URL and navigating to it using the `goto()` page method.

```
        # Navigate to the website
        url = "http://sandbox.oxylabs.io/products"
        page.goto(url)
```

### 6. Take a screenshot
Wait for the page to load completely, take the screenshot, and close the browser.

```
        # Wait for the webpage to load completely
        page.wait_for_load_state("load")

        # Take a screenshot
        screenshot_filename = "oxylabs_screenshot.png"
        page.screenshot(path=screenshot_filename)

        # Close the browser
        browser.close()

        print("Done! You can check the screenshot...")

capture_screenshot()
```

### 7. Execute and test
Here is what our complete code looks like:

```
# Import the required modules
from playwright.sync_api import sync_playwright
from playwright_stealth import stealth_sync

# Define the function to capture the screenshot
def capture_screenshot():
    # Create a playwright instance
    with sync_playwright() as play_wright:
        browser = play_wright.chromium.launch(headless=True)

        # Create a new context and page
        context = browser.new_context()
        page = context.new_page()

        # Apply the stealth settings
        stealth_sync(page)

        # Navigate to the website
        url = "http://sandbox.oxylabs.io/products"
        page.goto(url)

        # Wait for the webpage to load completely
        page.wait_for_load_state("load")

        # Take a screenshot
        screenshot_filename = "oxylabs_screenshot.png"
        page.screenshot(path=screenshot_filename)

        # Close the browser
        browser.close()

        print("Done! You can check the screenshot...")

capture_screenshot()
```

Note: Executing the code saves the screenshot.

## Bypass CAPTCHA with Web Unblocker

Oxylabs’ [Web Unblocker](https://oxylabs.io/products/web-unblocker) employs AI techniques to help you access publicly available information behind the CAPTCHA. You just need to send a simple query and Web Unblocker will automatically choose the fastest CAPTCHA proxy, attach all essential headers, and return the response HTML bypassing any anti-bots of the target websites.

### 1. Create an account
To use Web Unblocker, you'll need an active subscription. You can either get a paid plan or a 7-day free trial [here](https://dashboard.oxylabs.io/). 

### 2. Create API key
After successfully creating your account, you can set your API key username and password from the dashboard. These API key credentials will be used later in the code.

### 3. Install the requests module
You should use a library that can help perform HTTP requests. We will use the `requests` to send HTTP requests to Web  Unblocker API and capture the response.

```pip install requests```

### 4. Import the required modules
In your Python script file, import the modules using the following import statement:

```import requests```

Create the `proxies` dictionary to connect to Web Unblocker and then define the `headers` dictionary that’ll instruct Web Unblocker to use JavaScript rendering. See the [documentation](https://developers.oxylabs.io/advanced-proxy-solutions/web-unblocker) for more details. 

```
# Define proxy dict. Don't forget to pass your Web Unblocker credentials (username and password)
proxies = {
   "http": "http://USERNAME:PASSWORD@unblock.oxylabs.io:60000",
   "https": "http://USERNAME:PASSWORD@unblock.oxylabs.io:60000",
}

headers = {
    "X-Oxylabs-Render": "html"
}
```

### 6. Make a request
Perform your request by specifying the URL, request type, and proxy by using the following code.

```
response = requests.request(
   "GET",
   "http://sandbox.oxylabs.io/products",
   verify=False,  # Ignore the certificate
   proxies=proxies,
)
```

### 7. Save the response
Write the following code to print the response and save it in an HTML file.

```
# Print result page to stdout
print(response.text)

# Save returned HTML to result.html file
with open("result.html", "w") as f:
   f.write(response.text)
```

### 8. Execute and check
Execute the code and test the output. If the output HTML  file has actual page contents, the script successfully bypassed the CAPTCHA. Here is what our complete code looks like.

```
# Import the modules
import requests

# Define proxy dict. Don't forget to put your real user and pass here as well.
proxies = {
   "http": "http://USERNAME:PASSWORD@unblock.oxylabs.io:60000",
   "https": "http://USERNAME:PASSWORD@unblock.oxylabs.io:60000",
}

headers = {
    "X-Oxylabs-Render": "html"
}

response = requests.request(
   "GET",
   "http://sandbox.oxylabs.io/products",
   verify=False,  # Ignore the certificate
   proxies=proxies,
   headers=headers,
)

# Print result page to stdout
print(response.text)

# Save returned HTML to result.html file
with open("result.html", "w") as f:
   f.write(response.text)
```

And that's it! For a more detailed tutorial with images, you can check out this [article](https://oxylabs.io/blog/playwright-bypass-captcha). 
