WebGoat Write-Up: Bypass Front-end Restrictions
** Overview
  Client-side validation (validation done in the browser using HTML or JavaScript) is a common method used to guide users and ensure data is formatted correctly before it is sent to the server. However, because the client (the user's browser) has complete control over the environment, any security checks performed solely on the front-end can be easily bypassed.

** Objective: The goal of these exercises is to intercept HTTP requests, manipulate the data to bypass client-side restrictions, and send the altered request to the server. Applications must always validate input on the server-side.

** Tools Required:
A web browser (Chrome/Firefox).
An intercepting proxy tool (e.g., Burp Suite, OWASP ZAP, or the built-in WebGoat browser tools).

** Exercise 1: Field Restrictions
  * Task
    Send a request that bypasses restrictions on all five input fields:

     . Dropdown (Select)
     . Radio buttons
     . Checkbox
     . Input restricted to 5 characters
     . Read-only input field

** Steps to Solve
Navigate to the Field Restrictions lesson.

- Ensure your proxy (like Burp Suite) is configured to intercept traffic between your browser and the WebGoat application.
- Click the Submit button on the page.
- Go to your proxy tool and intercept the HTTP request. Forward it to the Repeater tab (or equivalent tool for editing).
  
**** Locate the POST request (similar to POST /WebGoat/BypassRestrictions/FieldRestrictions HTTP/1.1).***

- Look at the body of the request. It will contain the parameters for the fields. You will notice they contain default or valid values.

- Tamper with the parameters. Since the server is trusting the client, you can change the values to anything you want. Change the body to include invalid data: **** Original Example: select=Option1&radio=Option1&checkbox=on&shortInput=12345&readOnlyInput=change ***

** Tampered Example:

- select=Option3 (Add an option that doesn't exist in the HTML)
- radio=Option3 (Add an invalid radio option)
- checkbox=off (Or remove the parameter entirely)
- shortInput=ThisIsMoreThan5Characters (Exceed the limit)
- readOnlyInput=Hacked (Change the read-only value)
- Send the modified request.

***** The server will process the request and likely return a success message, indicating you have bypassed the front-end restrictions.****

** Exercise 2: Validation
 * Task
    Send a request that does not fit the regular expression (regex) constraints defined above the fields. The server is relying on client-side JavaScript to validate these fields before submission.

** Steps to Solve
- Navigate to the Validation lesson.
- Fill out the fields with valid data (e.g., Field 1: abc, Field 2: 123, Field 7: 301-604-4882). This ensures you can successfully click the "Submit" button.
  (Note: If you put invalid data now, the browser's JavaScript will block the request from being sent).
- Ensure your proxy is intercepting traffic.
-Click Submit.
- Intercept the HTTP request in your proxy and send it to the Repeater tab.

** The request body will contain the valid parameters. Modify the values in the request body to completely violate the regex rules stated on the page:

- Field 1 (exactly three lowercase): Change abc to ABC or 12345.
- Field 2 (exactly three digits): Change 123 to abc or 12.
- Field 3 (letters, numbers, space): Change abc 123 ABC to !!!invalid!!!.
- Field 4 (enumeration): Change seven to billion.
- Field 5 (5 digits): Change 01101 to 1.
- Field 6 (5 digits + optional dash 4): Change 90210-1111 to 999.
- Field 7 (US phone): Change 301-604-4882 to this-is-not-a-phone-number.
- Send the modified request.

Because the server does not validate the regex on its side, it will accept the malformed data, and you will complete the lesson.
