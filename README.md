# WebGoat Lab Write-up: Bypass Front-End Restrictions – Field Restrictions

## 1. Objective

The objective of this lab is to understand how front-end restrictions can be bypassed by modifying HTTP requests.

This exercise demonstrates that users can manipulate client-side HTML restrictions and submit modified values directly to the server using Burp Suite.

## 2. Tools Used

- WebGoat
- Burp Suite Community Edition
- Web Browser (Google Chrome)

## 3. Methodology

### Step 1: Configure Burp Suite and Proxy Settings

First, I opened Burp Suite and configured the browser proxy settings.

The proxy configuration was:

- Proxy Type: HTTP
- IP Address: 127.0.0.1
- Port: 8080

This configuration allowed Burp Suite to intercept HTTP traffic between the browser and WebGoat.

### Step 2: Submit the Form

I opened the WebGoat Field Restrictions exercise and filled in the required fields.

After completing the form, I clicked the Submit button to generate an HTTP request.

### Step 3: Capture the HTTP Request

I opened Burp Suite and navigated to:

**Proxy → HTTP History**

I searched for the following POST request:

`POST /WebGoat/BypassRestrictions/FieldRestrictions HTTP/1.1`

After finding the request, I right-clicked it and selected **Send to Repeater**.

### Step 4: Modify the HTTP Request

I opened the Repeater tab and inspected the captured HTTP request.

I modified the field values directly in the request body instead of relying on the restrictions imposed by the browser.

The fields included:

1. Select field
2. Radio button
3. Checkbox
4. Maximum-length input
5. Readonly input

I also examined how to modify values that did not match the specified regular expressions in the Validation exercise.

### Step 5: Send the Modified Request

After modifying the request, I clicked the **Send** button in Burp Suite Repeater.

I inspected the server response to determine whether the modified values were accepted.

## 4. Results

This exercise demonstrates that client-side restrictions can be manipulated by modifying HTTP requests before they reach the server.

It highlights the importance of implementing server-side validation rather than relying only on browser-side restrictions.

*Note: The actual success result should be confirmed by checking the WebGoat response.*

## 5. Conclusion

I learned how to use Burp Suite to intercept, inspect, and modify HTTP requests.

I also understood that HTML restrictions, such as maxlength, readonly, select options, and input validation, should not be considered security controls.

Developers should always implement proper server-side validation to prevent unauthorized or unexpected input values from being processed.
