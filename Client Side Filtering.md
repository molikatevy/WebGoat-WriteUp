WebGoat Write-Up: Client Side Filtering

** Overview: The core concept of these exercises is that applications often send more data to the client (your browser) than is visible on the screen. Even if data is hidden via HTML/CSS or removed from a dropdown menu, if it is present in the source code or the server response, a user can access it.

** Goal: Exploit extraneous information returned by the server to access data you are not supposed to see.

** Exercise 1: Salary Manager
- Scenario: You are logged in as Moe Stooge (CSO). You can view the salaries of other employees, but you should not be able to see the CEO's (Neville Bartholomew) salary. The application relies on hiding the CEO from the dropdown menu instead of securing the data on the server.

  * Task
- Find the CEO's salary and submit it.
(Based on WebGoat defaults, the answer is usually 450000, but let's find it properly).
- Steps to Solve (Using Browser Developer Tools)
- Navigate to the Salary manager page.
- Right-click anywhere on the page (or specifically on the "Select user" dropdown) and click Inspect (or Inspect Element).
- Open the Elements (or Inspector) tab in your browser's developer tools.
- Press Ctrl+F (or Cmd+F on Mac) to open the search bar within the HTML code.
- Search for #hiddenEmployeeRecords (as suggested in your screenshot) or simply search for "Neville".
- You will find a hidden HTML element containing a block of JSON or HTML data representing the employee database.
- Look through this code block to find the data tied to "Neville Bartholomew" and note his Salary.

 ** Return to the WebGoat page and type the salary amount into the "What is Neville Bartholomew's salary?" box, then click Submit Answer.**

** Exercise 2: No need to pay if you know the code... (Hidden Checkout Code)

- Scenario: You are looking at a product page (Samsung Galaxy S8). You want to buy it without paying. The application requires a "Checkout Code".

* Task
- Find the hidden checkout code to buy the phone for free.
- Steps to Solve (Using Browser Developer Tools)
- Navigate to the second lesson: No need to pay if you know the code... (Lesson 3 in the menu).
- Right-click on the page and select Inspect.
- Open the Elements tab.
- Click on the Network tab (if you want to see the raw response) OR simply use Ctrl+F in the Elements tab to search for words like "code", "checkout", or "hidden".
- You will find a hidden HTML input field or a JavaScript variable that contains the valid checkout code (e.g., get_it_for_free or a similar string).
- Copy that code.
- Paste the code into the CHECKOUT CODE field on the web page.
Click the green Buy button.
