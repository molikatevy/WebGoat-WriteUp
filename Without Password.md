WebGoat Write-Up: Challenge - Without Password

** Overview: The objective of this challenge is to log in as the user "Larry" without knowing his password. The application has a vulnerability in how it handles user input in the SQL query used for authentication. By inputting a specially crafted SQL payload, we can break the query and force the database to throw an error, which reveals the required flag.
** Objective: Log in as Larry and retrieve the flag to submit.
** Tools Required: An intercepting proxy tool (e.g., Burp Suite).
** Step-by-Step Solution
- Configure Burp Suite: Ensure Burp Suite is running and your browser is configured to proxy traffic through it. Turn Intercept ON.
- Setup the Login Attempt:
- Go to the "Without password" lesson.
- In the Username field, type: Larry
- In the Password field, type anything you want (e.g., password123).
- Optional: You can check the "Remember me" box.
- Intercept the Request: Click the Log In button.
- Send to Repeater: Go to Burp Suite, find the intercepted POST request (it will be to /WebGoat/challenge/5). Right-click and select Send to Repeater.

** Inject the SQL Payload:
- Go to the Repeater tab in Burp Suite.
- Look at the body of the request. You will see username=Larry&password=password123 (or similar).
- Modify the username parameter by adding a single quote (') at the end of Larry's name to break the SQL query syntax.
- Change the username value to: username=Larry'

*** (Example Body: username=Larry'&password=password123&remember-me=on)*** 
- Send the Request: Click Send in the Repeater tab.
- Analyze the Response: Look at the server's response in Burp Suite. Because the single quote breaks the SQL syntax, the application throws a Java SQL exception error.
- Extract the Flag: Within that error message, the database reveals the SQL query it was trying to run. Embedded in that error output is the "flag" (a long string of characters/numbers).
- Submit the Flag:
- Copy the flag.

Go back to the WebGoat browser window.

Paste the flag into the input box at the bottom of the page.

Click Submit result.
