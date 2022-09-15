JS Applications Exam – GamesPlay
You are assigned to implement a Web application (SPA) using JavaScript. The application should dynamically display content, based on user interaction and support user profiles and CRUD operations, using a REST service.
The application must start from file "index.html" on port 3000 and must be in .zip format (see Submitting Your Solution at the end of this document.)
Students from previous seasons attending this exam have the option to choose whether they will use the given REST service or use a cloud-based backend of their choice (Firebase, Backendless, etc.). As well as the libraries that will be used for rendering views/forms/components (Handlebars) or routing libraries (Sammy) depend on their preferences. 
⦁	Overview
Implement a front-end application (SPA) to see and manage the games world. The app allows visitors to browse different types of games, including the latest collections, with different levels of difficulty. Users can register with an email and password, which allows them to create their own games. Game authors can also edit or delete their own posts at any time.
⦁	Technical Details
You are provided with the following resources:
⦁	Project scaffold: A package.json file, containing a list of common dependencies. You may change the included libraries to your preference. The sections devDependencies and scripts of the file are used by the automated testing suite, altering them may result in incorrect test operation.
To initialize the project, execute the command npm install via the command-line terminal.
⦁	HTML and CSS files: All views (pages) of the application, including sample user-generated content, are included in the file index.html, which links to CSS and other static files. Each view is in a separate section of the file, which can be identified by a unique class name or id attribute. Your application may use any preferred method (such as a templating library or manual visibility settings) to display only the selected view and to navigate between views upon user interaction.
⦁	Local REST service: A special server, which contains sample data and supports user registration and CRUD operations via REST requests is included with the project. Each section of this document (where applicable) includes details about the necessary REST endpoints, to which requests must be sent, and the shape of the expected request body.
For more information on how to use the included server, see Appendix A: Using the Local REST Service at the end of this document.
⦁	 Automated tests: A complete test suite is included, which can be used to test the correctness of your solution. Your work will be assessed, based on these tests.
For more information on how to run the tests, see Appendix B: Running the Test Suite at the end of this document

Do not use CDN for loading the dependencies because it can affect the tests in a negative way!
Note: When creating HTML Elements and displaying them on the page, adhere as close as possible to the provided HTML samples. Changing the structure of the document may prevent the tests from running correctly, which will adversely affect your assessment grade. You may add attributes (such as class and dataset) to any HTML Element, as well as change "href" attributes on links and add/change the method and action attributes of HTML Forms, to facilitate the correct operation of a routing library or another method of abstraction. You may also add hidden elements to help you implement certain parts of the application requirements.
⦁	Application Requirements
Navigation Bar (5 pts)
Navigation links should correctly change the current page (view). GamesPlay link should redirect to the Home page. Guests (un-authenticated visitors) can see the links to the All Games (Catalogue) page, as well as the links to the Login and Register pages. The logged-in user navbar should contain the links to All Games (Catalogue) page, the Create page and a link for e Logout action.
Guest navigation example: 
 
User navigation example: 
 
Login User (5 pts)
The included REST service comes with the following premade user accounts, which you may use for development:
{ "email": "peter@abv.bg", "password": "123456" }
{ "email": "john@abv.bg", "password": "123456" }
The Login page contains a form for existing user authentication. By providing an email and password, the app should login a user in the system if there are no empty fields.
 
Send the following request to perform login:
Method: POST
URL: /users/login
Required headers are described in the documentation. The service expects a body with the following shape:
{
  email,
  password
}
Upon success, the REST service will return information about the existing user along with a property accessToken, which contains the session token for the user – you need to store this information using sessionStorage or localStorage, in order to be able to perform authenticated requests.
If the login was successful, redirect the user to the Home page. If there is an error, display an appropriate error message, using a system dialog (window.alert).
Register User (10 pts)
The Register page contains a form for new user registration. By providing an email and password, the app should register a new user in the system if there are no empty fields.
 
Send the following request to perform registration:
Method: POST
URL: /users/register
Required headers are described in the documentation. The service expects a body with the following shape:
{
  email,
  password
}
Upon success, the REST service will return the newly created object with an automatically generated _id and a property accessToken, which contains the session token for the user – you need to store this information using sessionStorage or localStorage, in order to be able to perform authenticated requests.
If the registration was successful, redirect the user to the Home page. If there is an error, or the validations don’t pass, display an appropriate error message, using a system dialog (window.alert).
Logout (5 pts)
The logout action is available to logged-in users. Send the following request to perform logout:
Method: GET
URL: /users/logout
Required headers are described in the documentation. Upon success, the REST service will return an empty response. Clear any session information you’ve stored in browser storage.
If the logout was successful, redirect the user to the Home page.
All Games Page (Catalogue) (10 pts)
This page displays a list of all games in the system, with their title and category. Clicking on any of the cards leads to the details page for the selected game. 
If there are no games, the following view should be displayed:
 
Send the following request to read the list of games:
Method: GET
URL: /data/games?sortBy=_createdOn%20desc
Required headers are described in the documentation. The service will return an array of games.
Home Page (Recent Games) (20 pts)
All users should be greeted from the homepage, where they should be able to see the three most recently added games. Clicking on the details links leads to the details page for the selected game. 
  








If no games have been added yet, show the text "No games yet" instead.
  
Send the following request to read the new games:
Method: GET
URL: /data/games?sortBy=_createdOn%20desc&distinct=category
Required headers are described in the documentation. The service will return an array of games. 
Create Game (15 pts)
The Create page is available to logged-in users. It contains a form for creating new games. Check if all the fields are filled before you send the request.
 
To create a game, send the following request:
Method: POST
URL: /data/games
Required headers are described in the documentation. The service expects a body with the following shape:
{
  title,
  category,
  maxLevel,
  imageUrl,
  summary
}
Required headers are described in the documentation. The service will return the newly created record. Upon success, redirect the user to the Home page.
Details (10 pts)
All users should be able to view details about games. Clicking the Details link in of a game should display the Details page:
⦁	If the currently logged in user is the creator of the game, the Edit and Delete buttons should be displayed, otherwise they should not be available.
⦁	The view for the creators should look like:
 





The view for guests and logged-in users should look like:
 
Send the following request to read a single game:
Method: GET
URL: /data/games/:id
Where :id is the id of the desired game. Required headers are described in the documentation. The service will return a single object.
Edit Game (15 pts)
The Edit page is accessible to logged-in users and allows the author to edit their own games. Clicking the Edit a specific game link on the details page should display the Edit page. It contains a form with input fields for all relevant properties. Make sure all fields are filled in before submitting the request. The fields must be filled in when the page is first loaded.
 
To edit a game, send the following request:
Method: PUT
URL: /data/games/:id
Where :id is the id of the desired game.
The service expects a body with the following shape:
{
  title,
  category,
  maxLevel,
  imageUrl,
  summary
}
Required headers are described in the documentation. The service will return the modified record. Note that PUT request do not merge properties and will instead replace the entire record. Upon success, redirect the user to the Details page for the current game.
Delete Game (10 pts)
The delete action is available to logged-in users, for game they have created. When the author clicks on the Delete action on any of their games, a confirmation dialog should be displayed, and upon confirming this dialog, the game should be deleted from the system.
To delete a game, send the following request:
Method: DELETE
URL: /data/games/:id
Where :id is the id of the desired game. Required headers are described in the documentation. The service will return an object, containing the deletion time. Upon success, redirect the user to the Home page.
BONUS: Comments (15 pts)
Every logged-in user should be able to comments other games, but not his own. 
Guest should not be able to see the section Add new comment, but should be able to see the section Comments The view for guests should look like: 
 
If there are no comments all users should see:
 
If there are comments all users should see:
 

Logged-in users see a form for adding a new comment. Every registered user can leave a comment under any games.  Authors can't comment on their own games.
The view when there are no comments yet and the user did not press [Add Comment] button should look like:
 


The view when the logged-in user add Comment to the game should look like:
 
Upon success, clear the content from the textarea field.
To load all comments for game, send the following request:
Method: GET
URL: /data/comments?where=gameId%3D%22{gameId}%22
Where {gameId} is the id of the desired game
To create a new comment, send the following request:
Method: POST
URL: /data/comments
The service expects a body with the following shape:
{
  gameId,
  comment
}
Where gameId is the id of the game, which the comment is associated with, and comment is the text content. Upon success, redirect the user to the same page.
