# Web with Python questions

## Software design
### Clean code
#### Point out 5 suggestions, how to format an SQL query!
- alignment
- indentation
- commenting
- one expression at one line
- using aliases
#### What layers can you name in a simple web application?
- View layer
    - this is the visible part of the application, user interaction happens at this layer
    - The type of interaction depends on the application. The application may only shows information, but it can have links, inputs etc
    - Technologies involved: HTML, CSS, Javascript
    - It communicates with the business logic layer (through forms, ajax)
- Business Logic layer
    - intermediate layer between view and data layer. It deals with the logic of the program
    - Receives data and transforms it, and also retrieves data
    - It performs required calculations
    - manages workflows (session management, user identification)
    - manages data access for the presentation layer
- Data layer
    - data used by the application is stored here
    - information comes from the business logic layer
    - when the information is received data retrieval will happen based on the given parameters. Then the data will be sent back
    - Technology used: SQL (postgreSQL,MySQL etc)
- Benefits of using layers is that it is easier to know which part does what. That makes the application easier to build, debug and maintain

### Error handling
#### What error can occur, when an array does not have an element on the requested index?
- IndexError
#### What is the “finally” block, and how would you use it?
- it will be executed at all times. Doesn’t matter if the except or try but is executed before it, the finally block will always be executed
#### Why should we catch special exception types?
- To only respond to errors that we think will occur. For example if we think an IndexError will happen, but if we catch all errors, then we won’t see different types of errors. And it is a problem because we might want to fix errors that are different than IndexError. And for that we have to know about them


### Security
#### What is SQL injection? How to protect an application against it?
- one of the most common web attacks to steal data 
- Inserting SQL statements to input fields for execution. The underlying SQL database will execute the query. Queries can be inserting to e.g. login forms
- this can lead to theft, modification or destruction of data. It is a major concern as credit cards, passports, sensitive records can be accessed
- To prevent
    - use input validation to only accept certain type, length, format, no standalone single quotation marks
    - sanitize data: modify the input to ensure it is valid, e.g. double single quotes
    - use character escape to escape e.g. quotation marks (e.g. username = username.replace("'", “’’”))
    - use query parameters instead of string interpolation
- Check if injection works: 
    - run the query: SELECT * FROM Users WHERE UserId = 105 OR 1=1;’ —> it’ll always be true
- We can also put a single quote to the input: if it says server error (or similar) then we can use sql injection. Single quotes should be escaped and if sql injection was taken care of we would get a reply as ‘there is no product with that name. 
- SELECT * FROM Users WHERE Name ="" or ""="" AND Pass ="" or ""=""
    - This query is valid and will return all rows from the "Users" table, since OR ""="" is always TRUE.
- SELECT * FROM Users; DROP TABLE Suppliers
    - it will return all rows from the users table and delete the suppliers table
#### What is XSS? How to protect an application against it?
- cross-site scripting
- the attacker injects client-side scripts to webpages
- changes the content of the page
    - e.g. <script>document.documentElement.innerHTML = “”</script>
- inject script to input fields
- sending the injected url to someone
- prevent
    - use innerText instead of innerHTML
    - escape user input -> stop certain characters to be rendered < >
    - validate input
    - sanitize data -> clean up harmful markups
#### How to properly store passwords?
- never store the password as plain text. Use hashing
#### What is HTTPS?
- Hyper Text Transfer Protocol Secure
- securing the communication between browser and web server
- while HTTP sends data in a hypertext format, HTTPS transfers it encrypted
- therefore credit card data or any sensitive information shouldn’t be sent over HTTP
- prevents hackers from reading and modifying data
#### What is encryption and decryption?
- Encryption: transforming the original information in a form that is not recognizable (creating Ciphertext)
    - done with encryption algorithm
    - makes data safe from stealing
- Decryption: convert Ciphertext data to readable form
    - security keys (or the password) are used to decrypt
#### What is hashing?
- Converting an input of any length into a fix size string of texts
- This is done using mathematical function
- A hash function transforms input to has value
- impossible to produce the same hash value by entering different inputs
#### What is the difference between encryption and hashing? When would you use which?
- Encryption is a 2 way function and makes it possible to decrypt the encrypted message. While hashing is one way and it is not reversible
- Hashing: 
    - store passwords
    - compare and avoid duplication
    - find a specific piece of data in a database (e.g. git commits)
- Encryption: sending data. If I’d like to send data someone encryption can protect it during transmission but the receiver can read it with a key
#### What encryption methods do you know?
- Advanced Encryption Standard (AES)
- Rivest-Shamir-Adleman (RSA)
- Triple Data Encryption Standard (TripleDES)
- Twofish
#### What hashing methods do you know?
- SHA1 - 160 bits 40 hexadecimal charcters. It is not considered safe as attacks can crack the algorithm
- SHA256 - 256 bits - 64 hexadecimal characters. One of the strongest hash function available. Based on SHA1. Fun fact: Bitcoin uses this algorithm
- MD5 - 128 bit 32 hexadecimal characters. not secure as it was reverse engineered
- Whirlpool - 512 bits - 128 digit hexadecimal characters
#### How/where would you store sensitive data (like db password, API key, ...) of your application?
- sensitive data should be stored either encrypted or hashed
- only store at trusted devices/services
- certain keys/passwords can be stored offline to prevent hackers from getting them

## Computer science
### Algorithms
#### What is the difference between Stack and Queue data structure?
- They are both ordered list of elements of similar data types. They are both linear data structures. The difference is between removing the data
- Stack:  FILO (First in Last out) e.g. function calls, scheduling algorithms
- Queue: FIFO (First in First out) - data inserted first will leave the queue first, e.g. ticketing
#### What is BubbleSort? Describe the main logic of this sorting algorithm.
- BubbleSort is a sorting algorithm
- uses a double for loop 
- checks if the first number is greater than the second. If it is, then the numbers swap. This checking iterates through all numbers and the iteration will result in the greatest number being at the last position of the list
- When the first iteration is over, a second will start. However, the iteration will be shorter by 1, as the last number is in the correct position. The iteration will check the first and second number and proceed accordingly. By the end, the second greatest number will be in position too
#### Explain the process of finding the maximum and minimum value in a list of numbers!
- create a variable with a value of 0, then iterate through the list
- within the iteration compare the variable and the current element. If its bigger/smaller than the variable, assign that value to it and then return at the end
#### Explain the process of calculating the average value in an array of numbers!
- add up the numbers (through iteration) and divide it by the length of the list
#### What is Big O complexity? Explain time and space complexity!
- describes how time scales with respect to some input variables
    - a way of describing how long an algorithm will run and how much memory is it going to use 
        - —> time and space complexity of an input code
- Complexity:
    - how the growth of certain inputs affects some resources
        - These resources can be time and memory
        - this makes complexity a function as the output is dependent on the input and it represents the rate of growth
- Time-complexity:
    - Finding the relationship between the size of the input and the time it takes it to run
    - to calculate it, we need to:
        - Measure how long it takes to get the first element: O(1). No matter the length of the input, this takes a constant time
        - Then we count the length of the input
        - With this we can find out the time it takes to run the code
- Memory/space complexity
    - it is the amount of memory that the algorithm uses
    - There are two important questions memory complexity aims to answer
        - What is the memory footprint of one element in the collection? e.g.1 byte
        - At any given time how many elements are in collections
- There are 4 rules to follow for simplification
    - Different steps get added
    - Drop constants 
        - O(2n) —> O(n). What matters is how things scale, e.g. is it linear, is it a quadratic relationship
    - Different inputs use different variables. Don’t use O(N^2) when e.g. there is a multiplication. Use O(a*b). Big O expresses how the runtime changes. Using a*b instead of N^2 is going to describe it better 
    - Drop non dominant terms: O(n+n^2) —> O(n^2). The biggest complexity matters
#### Explain the process of calculating the average value in a linked list of numbers!
- a linked list is a linear data structure. It is an ordered collection of data
- Unlike lists, elements in a linked list are not stored in a sequential order (meaning we cant index list[5] to get the 6th element). Instead they are linked together using a pointer
- Each node/element has their own data and a reference to the next node
- Each list starts with a head and ends with null
- Therefore, to calculate the average we do the following iterative solution
    - Initialise a pointer ptr with the head of the linked list and a sum variable with 0.
    - Start traversing the linked list using a loop until all the nodes get traversed.
    - Add the value of current node to the sum i.e. sum += ptr -> data .
    - Increment the pointer to the next node of linked list i.e. ptr = ptr ->next .
    - Divide sum by total number of node and Return the average.

### Procedural
#### How the CASE condition works in SQL?
SELECT something
    CASE
        WHEN something > 100 THEN ‘above hundred’
        WHEN something > 50 THEN ‘above fifty’
        WHEN something > 0 THEN ‘above zero’
        ELSE ‘below or equals zero’
    END as ‘number zone’
FROM table_of_something
#### How the switch-case condition works in JavaScript?
    - function basicOp(operation, value1, value2)
    {
     switch (operation){
            case '+': return value1+value2;
                break;
            case '-': return value1-value2;
                break;
            case '*': return value1*value2;
                break;
            case '/': return value1/value2;
                break;
          }
    }
- important to add break at the end of the cases to avoid fallthrough
#### How to achieve a switch-case-like structure in Python?
def switch_demo(argument):
    switcher = {
        1: "January",
        2: "February",
        3: "March",
        4: "April",
        5: "May",
        6: "June",
        7: "July",
        8: "August",
        9: "September",
        10: "October",
        11: "November",
        12: "December"
    }
    print switcher.get(argument, "Invalid month")
#### Explain variable scoping in Python!
- L - local
- E - enclosed (function inside another function)
- G - global
- B - built-in
- In python there is always a preference for local variables
- scope: where a variable is accessible
- lifetime: duration which the variable exists
#### What’s the difference between const and var in JavaScript?
- const was introduced in ES6
- const creates a constant (value cannot be changed)  while var create a variable
- var is only aware of global and function scope while const (and let) uses block level scope. Const cares about {}
- E.g
    - var name = ‘Bence’
    - 
    - if (name === ‘Bence’){
    - var hobbies = [‘Sleeping’]
    - }
    - console.log(name, hobbies) —> both would be logged
    - However if we use const or let inside the if block then the console.log would throw an error as hobbies not being defined
#### How the list comprehension looks like in Python?
- example = [x for x in lst] 
This is the same as:
- example = []
    for x in lst:
        example.append(x)
#### How the “ternary expression” looks like in Python?
a, b = 10, 20
min = a if a < b else b 
- min is set to 10
#### How the ternary expression looks like in JavaScript?
const userInput = “”; This would be undefined (falsy)
const isValidInput = userInput ? true : false
    - interpretation: if user input is true set isValidInput to true, if userInput is false then set it to false
#### How to import a function from another module in Python?
- from file import function
- from folder import file
    - file.function()
#### How to import a function from another module in JavaScript?
- first: export let dataHandler
- then: import {dataHandler} from "./data_handler.js";

### Functional
#### What is recursion?
- recursion is when a function calls itself
- it has the benefit that certain codes can be executed faster in this way
- the idea is to represent a problem in terms of one or more smaller problems, and add one or more base conditions that stop the recursion
- we can distinguish direct and indirect recursive functions
    - direct: the function calls the same function
    - indirect: the function calls a different function
- example for recursion is calculating factorial:
    - we can solve it the ‘normal way’
        def factorial(n):
                num = 1
                for i in range(1, n+1):
                    num *= i
                print(num)
    - with recursion it looks like this
        def fact_rec(n):
                if n == 1:
                        return 1
                else:
                       return n*fact_rec(n-1)
- it is important to mention that if the base is defined in a wrong way then recursion can cause stack overflow
    - e.g. in case in the following example, if n is 10 and we check if n == 100, then the function will cause stack overflow as it would never stop
#### Write a recursive function which calculates the Fibonacci numbers!
- def fib_rec(fn):
        if fn == 0:
                return 0
        elif fn == 1:
                return 1
        else:
                return fib_rec(fn-1) + fib_rec(fn-2)
#### How to store a function in a variable in Python?
    def do_something():
        print(‘do something’)
- function_in_variable = do_something()
- 
- def greet(name):
-  return "Hello " + name
- 
- greet_someone = greet
- print(greet_someone(“Bence”))
-  -Outputs: Hello Bence
#### List the ways of defining a callable logical unit in JavaScript!
- function something(){
    - console.log(‘something’)}
- const add = (a,b) => a + b
- const add2 = function(a,b){
    - return a+b;}
- something.addEventListener(‘click’, function (){}
- something.addEventListener(‘click’, () => {}
#### What is an event listener? How to attach one?
- In the browser a big part of the code is event driven and Javascript allows to write interactive applications, to handle such events. Event listeners react to such events, events that can make the application interactive. There’s a lot of different events we can handle, e.g.
    - click, double click, right click
    - hover
    - changes
- Event listeners listen to such events and react according to the function we provide to the event listener. Event listeners are callback functions
- listens to a click event. Then start a function which we add
- Attaching
    - In HTML: <button onclick="button is clicked"></button>
    - in JS:button.addEventListener(‘click’, () => {console.log(‘Hello’)} same as button.addEventListener(‘click’, someFunction)
#### How to trigger an event in JavaScript?
- Events are triggered (or fired) when the certain event is happening
- And when we catch that event, we call that event handling (handled)
#### What is a callback function? Tell some examples of its usage.
- e.g. at event listeners. We define a function and pass that function to the event listener. However, the function inside the event listener won’t be executed immediately, but only when the certain event occurs.
- Another example with API: when we make requests to an API, we have to wait for the response before we can act on that response
#### What is a Python decorator? How does it work? Tell some examples of its usage.
- decorators alter the functionality of a function (or method or class)
- it is beneficial because we can extend the functionality of a function without modifying it
    - they are wrappers to existing functions, changing the behaviour of a function before and after a target function execution
    - they augment the original function -> hence the name decorator
- it is possible to have more decorators on a function
    - order of setting matters
- can pass arguments as well
- python decorators use syntactic sugar, which means we can make the code a bit cleaner
    - instead of doing 
        - function_to_wrap = decorator(function_to_wrap)
        - function_to_wrap("John")
    - we can do
        - @decorator
        - def function_to_wrap(text_parameter):
        - return "Wrapped function. Its parameter: " + text_parameter
        - function_to_wrap("John”)
- an example for using decorators is for example when we use json data
    - we can write a function that converts the returned dictionary to a JSON response
    - then use that decorator to augment a function
        @json_response
        def get_boards():
                return data_handler.get_boards()
- we can also use python decorators. When we want to make operations on elements a database, we usually do the following:
    - connect to the database
    - run query to perform the operation
    - close the connection
- Decorators can help with the second part to create the connection, then create the cursor and passes the cursor to the decorated function. Then we save the return value of the decorated function and only return it when we close the cursor and the connection.
#### What is the difference between synchronous and asynchronous execution?
- asynchronous (async): will be executed later -> e.g. used at callbacks
    - start something now and finish it later
- synchronous: ‘normal’ function that is executed immediately

## Programming languages
### SQL
#### How can you connect your application to a database server? What are the possible ways?
- have to provide certain environment variables
    - user_name = os.environ.get('PSQL_USER_NAME')
    - password = os.environ.get('PSQL_PASSWORD')
    - host = os.environ.get('PSQL_HOST')
    - database_name = os.environ.get('PSQL_DB_NAME')
- Connect through terminal
- Connect by using sockets: sockets allow communication between two different processes on the same or different machines. It is a way to talk to other computers
- connect pycharm to flask (or other frameworks such as express)
    - for this we have to set up environmental variables, such as password, host, username, database
    - we can also use python decorators. When we want to make operations on elements a database, we usually do the following:
        - connect to the database
        - run query to perform the operation
        - close the connection
    - Decorators can help with the second part to create the connection, then create the cursor and passes the cursor to the decorated function. Then we save the return value of the decorated function and only return it when we close the cursor and the connection.
#### When do you use the DISTINCT keyword in SQL?
- when you want to get unique elements
#### What are aggregate functions in SQL? Give 3 examples.
- Aggregate functions return one value. E.g. returning the sum of the row values that matches a criteria
- Count, Sum, Min, Max
#### What kind of JOIN types do you know in SQL? Could you give examples?
Example: we have 
- users table with id, full_name, enabled, last_login
- addresses table with user_id, street, city, state 
- Inner: only returns rows where matches were found -> common elements of the tables
- if there is an entry in the first table, but there is no entry connected to it in the second then that wont show
        SELECT users.*, addresses.*
        FROM users
        INNER JOIN addresses
        ON users.id = addresses.user_id;
    
- Left: returns matches and all rows from the left listed table. It takes all rows from one table and joins with the second one. It will include rows that are from the LEFT table
- It means there can be null values at certain rows. 
- E.g. in this case if there is a user but there is no address connected to that person the the users columns will appear normal and the address columns will have a null value
        SELECT users.*, addresses.*
        FROM users
        LEFT JOIN addresses
        ON users.id = addresses.user_id;

- Right: returns matches and all rows from the right listed table. Similar to the left join, but the other way around
- Full: returns matches and all rows from both tables. It is a combination of LEFT JOIN and RIGHT JOIN
- Cross: returns all rows from one table crossed with every row from the second table. It contains every possible combination of rows from the tables that have been joined
- Natural: it is useful when the associated tables have one or more pairs of identically named columns. Natural join will return columns with the same name once. The syntax in this case is a bit different. We can omit the ON part:
    - SELECT*
    - FROM table1
    - NATURAL JOIN table2;
#### What are the constraints in sql?
- constraints are used to specify rules for the data in a table
- they limit the type of data that can go into the table
- helps to ensure data accuracy and reliability
- constraints can be table or column level
- Examples are:
    - NOT NULL: column cannot have a null value
    - UNIQUE: all values in a column are different
    - PRIMARY KEY: unique identifier for each row, a combination of not null and unique
    - FOREIGN KEY: uniquely identifies a row/record in another table
#### What is a cursor in SQL? Why would you use one?
- A cursor can be viewed as a pointer to one row in a set of rows and can only reference one row at a time, but can move to other rows of the result set as needed
- We could use it when we want to fetch records row by row. It is useful for data retrieval
    - SQL commands operate on all rows in the result set, cursors help to operate on them one by one
- acts like a looping statement
- we can do operations while traversing such as delete or insert
#### What are database indexes? When to use?
- It allows queries to efficiently retrieve data from a database
- They are related to specific tables and consists of one or more keys (values we want to look up in the index)
- E.g. consider the index in the back of a book. We use it by looking for the subjects we’re interested in, note, and flip to those pages in the book.
- The keys to this index are the subject words we reference.  The index entries consist of the key and page numbers.  The keys are in alphabetical order, which makes really easy for us to scan the index, find an entry, note the pages, and then flip the book to the correct pages.
- The power of the index is that it allows more or less direct access to the book’s pages we’re interested in seeing.
#### What are database transactions? When to use?
- A transaction is a unit of work that you want to treat as "a whole." It has to either happen in full or not at all.
- For example:
    -  transferring money from one bank account to another. To do that we have first to withdraw the amount from the source account, and then deposit it to the destination account. The operation has to succeed in full, we cannot stop halfway
    - The basic idea of transactions is that transactions are there to ensure, that no matter what happens, the data you work with will be in a sensible state. Transactions guarantee that there will NOT be a situation where money is withdrawn from one account, but not deposited to another.
#### What kind of database relations do you know? How to define them?
- One-to-one
- One-to-many and vice versa
- Many-to-many
- We can use keys to connect the tables and set up a relationship between them
    CREATE TABLE customers (
            customer_id INT AUTO_INCREMENT PRIMARY KEY,
            customer_name VARCHAR(100)
    );

    CREATE TABLE orders (
            order_id INT AUTO_INCREMENT PRIMARY KEY,
            customer_id INT,
            amount DOUBLE,
            FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
    );
#### You have a table with an “address” field which contains data like “3525, Miskolc, Régiposta 9.” (postcode, city, street name and address). How would you query all records related to Miskolc?
- SELECT * FROM table WHERE address LIKE ‘%Miskolc%’
#### How would you keep track of what kind of data has changed after an UPDATE or DELETE operation in a table?
- use logs to keep track of changes (use audit tables)
- we can also track changes by having a separate table that gets an entry added to it by triggers on INSERT/UPDATE/DELETE statements

### HTML & CSS
#### What’s the difference between XML, XHTML and HTML?
- HTML - original language of WWW
- XML and HHTML 
    -  bigger vocabulary than HTML
    - strict error handling
#### How to include a JavaScript file in a webpage?
- usually in the header section (but can be at other places of the code too)
- <script src =“” filename=“” defer></script>
#### How to include a CSS file in a webpage?
- in the header section
- <link rel=‘stylesheet’ type=“text/css” href=“”>
#### How to select an element using its id in CSS?
- #
#### How to select elements using their class in CSS?
- .
#### How to select elements which have the ‘alpha’ and ‘beta’ classes in CSS?
- .alpha.beta{color:red;}
#### How to select all list items in all ordered lists on the page in CSS?
- ol > li —> selects direct child li within ol
- ol li —> selects all nested li within ol
#### How to select elements using their attributes in CSS?
- using brackets, e.g.:
- input[id=‘red’] {do stuff}
    - this only selects the input element that has the ‘red’ id attribute
#### What are UX and UI?
- UX: user experience
    - focus on usability, responsive design
- UI: user interface design
    - Laws describing how humans typically see objects
    - focus on looks
#### Please list some points that an application should fulfil to have good UX.
- understand the page at first glance
- looks good on different screen sizes
#### What is XML, XSLT, DTD?
- XML: eXtensible Markup Language
        - store and transport data
        - information wrapped in tags (which are not predefined)
        - stores data in plain text format. This provides a software- and hardware-independent way of storing, transporting, and sharing data
- XSLT: change XML files
- DTD: document type definition. It’s a standard. There are other standards as well
    - defines structure of elements and attributes of an XML document
    - helps people to agree on standards
#### What is the difference between HTML and XML?
- tags (predefined and not) - XML tags are not predefined, while HTML tags are
- HTML is for displaying data while XML is for carrying. Focus on how the data looks (HTML) vs. what the data is (XML)

### Javascript
#### What is javascript?
- a programming language
- on contrary to the name it is not connected to java
#### When to use AJAX? Bring examples of its usage.
- AJAX:Asynchronous JavaScript and XML
- It is a web development technique to send and retrieve data without refreshing the webpage
- It doesn’t load data through the url bar initiated HTTP request, but through JavaScript XML HTTP request object (XHR). Eventually it makes http requests behind the scene without reloading the whole page
- Example: When we check out our Facebook news feed and we see a picture/post it shows how many people have commented. We can click on a button to expand that section and see the comments and vice versa. This happens without needing to refresh the whole web page
#### What is DOM and how to manipulate it from Javascript?
- Document Object Model
- with js we can change html elements, their attributes, css styles
- manipulate:
    - for example select an element: let test = document.getElementById(‘practice’) —> this selects the element that has the practice id attribute
    - next step: test.style.backgroundColor = ‘black’ —> sets the background to black
    - test.innerText = ‘new text’ -> changes the text
#### What are events and how/why to use them in Javascript?
- There are a lot of different events such as clicks, scrolls, hovers, changes etc
- Events are important because most of the code in browsers are event driven. And to make our webpage interactive we need code that reacts to these events. We use eventListeners for that. Event listeners wait for an event to happen and then alter certain things in the browser. 
- For example if we have a long website we want to user to see everything, even content that doesn’t fit on the screen. We can add an event listener that captures scrolling and loads content accordingly
#### What is event bubbling/capturing? How would you use it?
- When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.
    - This process is called “bubbling”, because events “bubble” from the inner element up through parents like a bubble in the water.
- e.g. When we click on the <p> tag there will be three alerts in the following order: p -> div -> form
    <form onclick="alert('form')">FORM
          <div onclick="alert('div')">DIV
                <p onclick="alert('p')">P</p>
          </div>
    </form>
- we can stop this by using: event.stopPropagation()
- in order to get details about the elements we can use event.target and event.CurrentTarget
    - event.target is what triggers the event dispatcher to trigger and event.currentTarget (=this) is what you assigned your listener to
- Capturing: 
    The standard DOM Events describes 3 phases of event propagation:
    - Capturing phase – the event goes down to the element.
    - Target phase – the event reached the target element.
    - Bubbling phase – the event bubbles up from the element.
    - So for example:  for a click on <td> the event first goes through the ancestors chain down to the element (capturing phase), then it reaches the target and triggers there (target phase), and then it goes up (bubbling phase), calling handlers on its way
#### What is JSON and how do we use it?
- JavaScript Object Notation
- Uses key: value pairs
- Data representation format, like xml
- Common use is for APIs and Configs
- Small file size and easy to read and write because there’s not many opening and closing tags
- Integrates well with JavaScript, because anything we write in JSON is valid in JS. Apart from JS most languages also work well with JSON
- Big benefit: possible to deeply nest properties
- example: codecoolers.json
    - [
        - {
        - “name”:”Bence”,
        - “joined”: 2019
        - },
        - {
        - “name”:”Codecooler”,
        - “joined”:2020
        - }
    - ]
    - Most of the times we get JSON file as a string. We have to use JSON.parse() to convert to JS object

## Software engineering
### Version control
#### What type of branching strategy would you use?
- GitFlow workflow. It uses the following branches: 
- There should be a master (doesn’t have to be named master) branch that is the latest version of the working application. Continuous development doesn’t happen on this branch
- Development branch: this is the (usually) unstable version of the application. This is where continuous development happens.
- Feature branch: a branch where developers work on a new feature. These branches are branched off from development branches and upon finishing them, merge them to that branch
- Release branch: supports the preparation of a new release. Developers can work on fixing bugs. It is free from development branch, therefore the development branch can receive new features that are intended for the next release. When the release branch is stable then it gets merged to the master branch
- Hotflix branches: they can help with the release branch, however they also needed when a critical bug is found in the master version of the code. In this case, a hotflix branch should be created from the master branch, because the master branch reflects the last desirable state of the application in production. When the bug is resolved the branch should be merged to master. Furthermore, it should be merged to the development branch as well so that the bug is fixed in that version as well
#### What would you do if you find a bug on the production code (master branch)?
- In this case, a hotflix branch should be created from the master branch, because the master branch reflects the last desirable state of the application in production. When the bug is resolved the branch should be merged to master. Furthermore, it should be merged to the development branch as well so that the bug is fixed in that version as well
#### How can you move changes from one branch to another in GIT?
- Either by merging
- or checkout the current branch end then create a new branch. When we checkout the new branch it will have the same contents as the one before (at this state it is a duplicate branch)
#### How does a VCS help with code reviews?
- The person that does the review doesn’t have to download our code, he/she can view in online in our repository
- Can comment on code sections (or start a review, conversation)
    - can also combine comments which can help the reader to understand our thoughts and recommendations better
- Can request for changes when merging
- We can ask for review which makes it possible to make sure every code gets reviewed
- GitHub creates a list of the approvals and requests for changes, which helps in getting a better overview
#### What is your favorite git command? Why?
- git push. It feels good when a feature is ready and I get to push it and share with others :)
#### What does remote/local mean in Git? 
- local: repositories are at my personal working directory on my computer
- remote: repositories at e.g. GitHub, BitBucket 
- we can connect local and remote repositories, then push local changes to remote directories and also pull changes. -> basically allows to work on a project as a group

### DevOps
#### Why is it good to use a package manager software?
- helps with complex dependencies
- helps to check if there is a new version available
- helps to know which libraries and which version we use
    - easier to identify it we need to update a library due to a bug/security issue
- transitive dependencies are updated as well
#### Why is it good to use a virtual environment for a project?
- stay away from dependency conflicts
- It is possible to install a different version of a package to a different project

### Networks
#### What kind of HTTP status codes do you know?
- 1xx: information response e.g. the request was received
- 2xx: successful: 200 - ok, 201 - created, 202 - accepted
- 3xx: redirect, further action is needed to complete the request
- 4xx: client side error, e.g. bad syntax. E.g. 404: not found, 403 forbidden, 400 bad request
- 5xx: server side error. E.g. 500: internal server error in case of unexpected condition
#### What is an API?
- Application Programming Interface
- lets us connect to the outside world
- E.g. Python is an interface that allows to use an external module (that is not on our computer but on a network) such as Flask
- We can send a request and get data back (usually in JSON)
- E.g. Momondo, Skyscanner etc. use API-s to get data for their website from different websites
#### What is REST API?
- REpresentational State Transfer
- can make GET, POST, PUT, DELETE requests to create, read, update, delete data
- Treat URL-s as access points to resources on the server
    - example.com/users -> users are the resource
    - requests on this url act on the whole users resource
- example.com/users/1 -> only acts on a single user e.g GET, DELETE
#### What is JSON? When to use?
- JavaScript Object Notation
- Uses key: value pairs
- Data representation format, like xml
- Common use is for APIs and Configs
- Small file size and easy to read and write because there’s not many opening and closing tags
- Integrates well with JavaScript, because anything we write in JSON is valid in JS. Apart from JS most languages also work well with JSON
- Big benefit: possible to deeply nest properties
- example: codecoolers.json
    - [
        - {
        - “name”:”Bence”,
        - “joined”: 2019
        - },
        - {
        - “name”:”Codecooler”,
        - “joined”:2020
        - }
    - ]
    - Most of the times we get JSON file as a string. We have to use JSON.parse() to convert to JS object
#### What is TCP/IP? What layers does it define, what are they responsible for?
- Transmission Control Protocol/Internet Protocol
- it helps in understanding how a specific computer should be connected to the internet and how data should be transmitted between them
- the basic purpose of TCP/IP is to allow communication between large distances
- it is designed as a model to offer highly reliable and end-to-end byte stream over an unreliable internetwork
- the most important characteristics of this protocol are
    - easy to add more systems to the network
    - flexible architecture support
    - the network remains intact until the source, and destination machines are functioning properly
- There are four layers. It is important to know that TCP/IP is is a layered server architecture system where each layer is defined according to a specific function it should perform. These layers work together to transmit data from one layer to the other
    - Application/process layer: allow access to the network resources. The user interacts with the software through this layer
    - Transport/host-to-host layer: provide reliable process in order to process message delivery and error delivery. Determines how much data should be sent and where at which rate
    - Internet layer: it moves packets from source to destination
    - Network access/link layer: it is responsible for the transmission between two devices on the same network. Define details how data should be sent. Also includes how bits should be signalled by hardware devices that uses network mediums such as coaxial, optical, fiber etc cables
#### What’s the difference between TCP and UDP?
- They are both protocols but they are used for different types of data
- TCP/IP: a protocol used by devices to communicate over the internet and local networks. It allows apps to deliver an ordered and error-checked stream of information packets over the network
    - Reliability is key here: packets sent with TCP are tracked so no data is lost or corrupted in transit
    - TCP achieves this in two ways. First, it orders packets by numbering them. Second, it error-checks’’
    - e.g. when clicking on a link a link, sign in, post a comment
- UPD (User Datagram Protocol): used by apps to deliver a faster stream of information, by not using error-checking
- back-and-forth communication introduce latency, and UDP throws this communication out. It also means data can be lost
- UDP is used when speed is desirable and error correction isn’t necessary. For example, UDP is frequently used for live broadcasts and online games
#### How does an HTTP Request look like? What are the most relevant HTTP header fields?
- An HTTP request is one case of a general HTTP message. We can make a request to the server to receive a certain file, image, html back
- An HTTP message has a start line, headers and body
- Headers
    - Host (google.com)
    - Patch(/images/logo.jpg)
    - Cookies (string)
    - accept-language
    - user-agent(string -> our browser, computer details)
    - Content type (application/json)
- e.g. making a request to codecool.com
    - Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
    - Accept-Encoding: gzip, deflate, br
    - Accept-Language: hu-HU,hu;q=0.9,en-US;q=0.8,en;q=0.7,da;q=0.6
    - Cache-Control: no-cache
    - Connection: keep-alive
    - Cookie: __cfduid=d59034deab8867e1b25782c8b9d66df031568731014; _ga=GA1.2.1654404729.1568731018; _hjid=91354607-8c75-44b0-a680-a246375ba654; _fbp=fb.1.1568731021393.551277369; livecall-account-8682=6a16833f-abe6-4850-a0ec-9c1f5e4fcbe0; livecall-account-6303=d353c0b8-b0a6-4374-bae9-295179cf5899; prism_475621117=c2f881f2-f37c-4730-b405-b68a7043b187; _gcl_au=1.1.1207586049.1586453660; PHPSESSID=ugu9qfdasohhknllh7d4hk4fq1; _fbc=fb.1.1590132099629.IwAR2P_QcWxK2J8_nXwQ-rNkQsZxfhixNPHLLkxVSpg-HOWwxLOgD1PGBDhUE; cookieLaw=1; _icl_current_language=hu; _gid=GA1.2.886280280.1590231323; _hjAbsoluteSessionInProgress=1
    - Host: codecool.com
    - Pragma: no-cache
    - Sec-Fetch-Dest: document
    - Sec-Fetch-Mode: navigate
    - Sec-Fetch-Site: none
    - Sec-Fetch-User: ?1
    - Upgrade-Insecure-Requests: 1
    - User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.129 Safari/537.36
#### How does an HTTP Response look like? What are the most relevant HTTP header fields?
- A response happens after we make a request
- Response can be an html page, image, css file etc. Our browser knows what it is getting by the content type. The server gives us the file and the content type. When this happens our browser can start the parsing process
- Headers
    - Content type (text/html, image/jpg, application/json)
    - Status/Code (200-ok 400-not found 500-error)
- Response from codecool.com
    - alt-svc: h3-27=":443"; ma=86400, h3-25=":443"; ma=86400, h3-24=":443"; ma=86400, h3-23=":443"; ma=86400
    - Cache-Control: no-store, no-cache, must-revalidate
    - CF-Cache-Status: DYNAMIC
    - CF-RAY: 597e4f5bcdaad40f-BUD
    - cf-request-id: 02e2cfed5d0000d40f4bb25200000001
    - Connection: keep-alive
    - Content-Type: text/html; charset=UTF-8
    - Date: Sat, 23 May 2020 11:06:52 GMT
    - Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
    - Expires: Thu, 19 Nov 1981 08:52:00 GMT
    - Location: https://codecool.com/hu
    - Pragma: no-cache
    - Server: cloudflare
    - Transfer-Encoding: chunked
    - X-Powered-By: PHP/7.3.3
    - X-Redirect-By: WordPress
#### What is DNS? How does it work?
- Domain Name System
    - IP address: computer identifiers e.g. 192.168.1.1
    - Computers use such numbers 
    - On the other hand, people use names
    - DNS is used to translate actual names to these numbers, it resolves domain names to IP addresses
        - e.g. when we type in a name to the browser, DNS will resolve it to a number
    - When we type in a certain domain name to the browser the DNS server is going to search through its database to find a matching IP address for that domain name
        - It is similar to a phone book: when we want to call someone we look up that person’s name, not their phone number. When we found that person then we have the number as well
- The way it works:
    - first it tries to find the match in the web browsers cache
    - it it cant find, then it sends a query to the resolver server. It is basically our ISP (internet service provider). When they receive the query then they will search their cache
    - in case they cant find it, they send a query to the root server. Root servers are the top of the DNS hierarchy. There are sets of root servers placed around the world.
    - Root servers don’t know the matches, but they can direct the resolver to the TLD (top level domain) server, e.g. .com, .net, .org. Now the resolver can ask for the ip address from the TLD. 
    - However, the TLD doesn’t know the address either, it will direct the resolver to the final level, to the Authoritative Name Server. These servers are responsible for knowing details about the domain and are able to give the IP address to the resolver. After this, the resolver is finally able to tell our computer the IP address for the certain domain name and now our computer can retrieve the webpage. 
    - This whole process seems to be a lot, but in reality it is very fast. On top of that, after the resolver receives the address, it will store it in it’s cache so that it doesn’t have to go over this process again
#### What is a web server?
- It listens for a request for a webpage
- A web server is a software that runs on a computer and when we ask for a web page the web server puts the raw materials such as images, files, html together, into a webpage. 
    - Then it sends back to our computer.
- Nowadays most hosts have a web server installed that is configured for us
- There are two different type of web servers:
- Static: consists of a computer (hardware) with an HTTP server (software). We call it "static" because the server sends its hosted files "as-is" to our browser.
- Dynamic: consists of a static web server plus extra software, most commonly an application server and a database. We call it "dynamic" because the application server updates the hosted files before sending them to our browser via the HTTP server.(the example I wrote at the beginning)
#### Explain the client-server architecture.
- It is a specific architecture and structure for communication
- The client-server architecture is a computing model, where the server hosts, distributes and controls the majority of the resources as well as services to be used by the client
- In this architecture, when the client computer sends a request for data to the server through the internet, the server accepts the request, processes it and delivers the data packets requested back to the client. 
    - e.g. we make a request for a website to get weather information
    - One special feature is that the server computer can manage several clients simultaneously, whereas one client can be connected to several servers at a time, each providing a different set of services.
- In its simplest form, the internet is also based on client/server architecture where web servers serve many simultaneous users with website data.
#### What would you use a cookie for?
- a cookie is a small piece of data sent from a website and stored on the user's computer by the user's web browser while the user is browsing
- for security reasons cookies can only be set on the current resource's top domain and its sub domains
- there are two types of cookies
    - session cookies, which store string values and will be deleted when the browser closes
        - user preferences, e.g. theme
    - persistent cookies
        - it has an expiry attribute, which means it will be deleted after a specific time
- cookies are mostly used to store non-sensitive data as users can have access to them and can tamper them
    - therefore they are mostly used for preferences
    - personalized ads also show up based on cookies
- cookies are supported by all browsers
- they can have a maximum size of ~ 4kb
- cookies use key: value pairs
#### What would you use a session for?
- Cookies are stored on the client side, meaning they can modify it
- Sessions are used when we want to store data about users and we don’t want them to tamper with it or be only accessible by the server
- We can store such data on the server side
- It is possible to store greater amount of data about the user
- Only keep temporary data in sessions that tracks that current user
- However since HTTP is stateless (HTTP is called as a stateless protocol because each request is executed independently, without any knowledge of the requests that were executed before it) we need a way to associate a request to any other request, we need a way to store user data between HTTP requests. We use cookies for that, so we authenticate the user with a cookie and based on that we can show the data from the server's data source. 
    - The solution is to store that data server side, give it an "id", and let the client only know (and pass back at every http request) that id.
- In this case the user id is stored in the session data, server-side, after successful identification. Then for every HTTP request we get from the client, the session id (given by the client) will point us to the correct session data (stored by the server) that contains the authenticated user id - this way the code will know what user it is talking to


## Software Development Methodologies
#### What kind of software development methodologies do you know? What are the main features of these?
- waterfall
    - rigid and linear model which consists of sequential phases (requirements, design, implementation, verification, maintenance)
    - phases must be completed before the next one can be started
    - no process of going back and modify the project
- agile
    - develop the software in iterations which contains mini-increments of the new functionality
    - allows software to be released in iterations. It helps in finding and fixing bugs early and also help in aligning expectations
    - users can realise certain software benefits earlier
    - there are different forms such as scrum, extreme programming, crystal
#### What are the SCRUM roles?
- product owner
    - define project backlog items
    - prioritise items
    - accepts/rejects work
    - answers questions and delivers information
- development/delivery team
    - participate in scrum ceremonies
    - implement backlog item tasks
    - write unit tests
    - present the implemented tasks
- scrum master (delivery team member)
    - ensures team productivity
    - communicate with product owner
    - responsible for following scrum processes
        - schedule meetings such as planning, code review, retrospective, daily stand up
        - documenting 
#### What are the SCRUM ceremonies?
- sprint planning: the team meets and decides what to complete for the sprint
- daily scrum: a short daily meeting to make sure everyone is on the same page
- sprint review: the team demos what they shipped during the sprint
- sprint retrospective: reviewing work, identify what went well and what didn’t so that they can make the next sprint better
#### What are the SCRUM artifacts?
- help in solving problems
- three main artifacts
    - product backlog
        - contains baseline requirements in a prioritized way
        - the PO is responsible for the content and validity
        - it can be subject to change (e.g. during product backlog refinement)
        - each item must align to the overall product roadmap
    - sprint backlog
        - subset of the product backlog
        - the team works on these tasks during the sprint
        - “to do list”
        - items are further broken down into tasks
        - backlog items must be developed, tested, documented and integrated
    - increment
        - usable end product from the sprint
        - show it during demos
        - must align with the ‘definition of done’, a common team agreement as what constitutes done
#### What is the main goal of a retrospective meeting?
- to discuss what went well and what did not
#### Explain, when would you recommend to use the waterfall methodology?
- requirements are extremely clear and fixed
    - the project has strict requirements and regularions
- an organization has strict processes
- product owner involvement is low
- enhancing an existing product (as opposed to a greenfield product)
- fixed and firm timeline
- fixed and inflexible budget
- more predictable what the team is going to deliver

