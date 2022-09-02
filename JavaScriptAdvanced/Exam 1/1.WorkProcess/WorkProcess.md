Problem 1. Work Process
Environment Specifics
Please, be aware that every JS environment may behave differently when executing code. Certain things that work in the browser are not supported in Node.js, which is the environment used by Judge.
The following actions are NOT supported:
⦁	.forEach() with NodeList (returned by querySelector() and querySelectorAll())
⦁	.forEach() with HTMLCollection (returned by getElementsByClassName() and element.children)
⦁	Using the spread-operator (...) to convert a NodeList into an array
⦁	append() in Judge (use only appendChild())
⦁	replaceWith() in Judge
⦁	replaceAll() in Judge
⦁	closest() in Judge
⦁	replaceChildren()
⦁	Always turn the collection into a JS array (forEach, forOf, et.)
If you want to perform these operations, you may use Array.from() to first convert the collection into an array. 
Use the provided skeleton to solve this problem.
Note: You can't and you have no permission to change directly the given HTML code (index.html file).
 
Your Task
Write the missing JavaScript code to make the Work Process work as expected:
⦁	Getting the information from the hired form
 
⦁	All fields are non-empty strings. If any of them are empty, the program should not do anything.
⦁	When you click the ["Hire Worker"] button, the information from the input fields must be added to the table and then clear input fields. 
⦁	Each input must be saved in td tag and the end must be added buttons – Fired and Edit. Look at the example below.
⦁	The HTML structure looks like this:
 
 
⦁	When the record is saved the salary must be added to the budget message. The sum should be rounded to the second decimal number:
 
 




⦁	Edit information for workers
⦁	When the ["Edit"] button is clicked, the information from the table must be sent to the input’s fields and the record should be deleted from the table. 
⦁	The salary for the edit worker should be taken out from the budget.
 
⦁	After editing the information make a new record to the table with updated information.
 





⦁	Fired workers
⦁	When you click the ["Fired"] button, the record must be deleted from the table;
⦁	The salary for the fired worker should be taken out from the budget.
 
Submission
Submit only your solve() function.
GOOD LUCK… 
