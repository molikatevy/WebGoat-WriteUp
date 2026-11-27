WebGoat Write-Up: Challenge - Admin password reset

** Overview: The objective of this challenge is to reset the administrator's password without having access to the admin's email inbox. Because the application's source code is open-source, we can inspect it to find the hardcoded hash value used to generate password reset links.
** Objective: Reset the admin's password and retrieve the flag.
** Tools Required: 
- WebWolf (WebGoat's companion application for simulating email).
- A web browser (to access GitHub).

** Step-by-Step Solution
- Part 1: Trigger the Password Reset
    - Navigate to the "Admin password reset" challenge.
    - In the "email address" field, enter any email address you have access to in WebWolf (e.g., yourname@webgoat.org or whatever email is associated with your WebGoat session).
    - Click the Reset Password button.
    - Open a new tab and navigate to your WebWolf application (usually running on port 9090, e.g., http://localhost:9090/WebWolf).
    - Go to the Inbox (or Mailbox) section. You will see an email containing a password reset link.
    - Analyze the Link: The link will look something like this:
    http://localhost:8080/WebGoat/challenge/7/reset-password/<Hash_Value>
    - Copy the <Hash_Value> (the long string of letters and numbers at the end of the URL). We will need to replace this with the Admin's hash.

- Part 2: Find the Admin's Hash (White Box Testing)
    - Open a new tab and go to the WebGoat GitHub repository.
    - Navigate to the source code file for this specific challenge. Based on the screenshot, the path is:
    webgoat-lessons/challenge/src/main/java/org/owasp/webgoat/challenges/challenge7/Assignment7.java
    - Read through the Java code. You will see a reference to import org.owasp.webgoat.challenges.SolutionConstants;.
    - Search the repository (or use the direct link in the screenshot) to open SolutionConstants.java.
    - Inside this file, you will find the hardcoded hash value used for the admin password reset. It will look like this: 375afe1104f4a487a73823c50a9292a2.
    - Copy this hash value.

- Part 3: Exploit the Vulnerability
    - Go back to the URL from Step 6.
    - Replace your original hash with the admin's hash. The URL should now look like this:
    http://localhost:8080/WebGoat/challenge/7/reset-password/375afe1104f4a487a73823c50a9292a2
    - Press Enter to navigate to this URL.
    - The page will prompt you to enter a new password for the admin. Type a new password and submit it.
    - The application will confirm the password was changed and display the Flag.
    - Copy the flag, go back to the WebGoat challenge page, paste it into the input box at the bottom, and click Submit result.
