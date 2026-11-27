WebGoat Write-Up: HTML Tampering

** Overview: This lesson demonstrates a critical vulnerability where an application relies on the client side (the browser) to calculate or provide sensitive data, such as the price of an item. Because the user has full control over their browser and the data being sent to the server, they can tamper with the values before submission.
** Objective: Purchase a TV for a lower price by intercepting and modifying the HTTP request before it reaches the server.
** Tools Required: An intercepting proxy tool (e.g., Burp Suite, OWASP ZAP, or Browser Developer Tools).
** Step-by-Step Solution
- Configure your Proxy: Ensure your browser is configured to send traffic through your proxy tool (like Burp Suite) and that "Intercept" is turned ON.
- Initiate Checkout: On the WebGoat page, review the shopping cart. You will see a TV priced at $2999.99. Click the green Checkout button.
- Intercept the Request: Go to your proxy tool. You will capture a POST request going to the WebGoat server (similar to POST /WebGoat/HTMLTampering/task HTTP/1.1).
- Send to Repeater: Right-click the intercepted request and select Send to Repeater (or equivalent tool for editing).
- Analyze the Body: Look at the parameters in the body of the request. You will see variables that define the order, such as:
    - QTY=1
    - Total=2999.99
- Tamper with the Data: Change the value of the Total parameter to something lower (e.g., Total=1.00 or Total=0).
- Send the Modified Request: Click Send in your proxy tool.

** Verify Success: Look at the server's response in your proxy tool. If it indicates success, switch back to WebGoat (turn off interception first if needed) and you should see the lesson marked as complete.
