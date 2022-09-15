## Music App

### Navigation Bar (10 pts)
Navigation links should correctly change the current page (view).  
The Home link should redirect to the Home page.  
Guests (un-authenticated visitors) can see the links to the Catalog page, the Login and Register pages.  
The logged-in user navbar should contain the links to the Catalog page, the Create page, and a link for e Logout action.    
![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  

### Login User (5 pts)
The included REST service comes with the following premade user accounts, which you may use for development:  
{ "email": "peter@abv.bg", "password": "123456" }  
{ "email": "john@abv.bg", "password": "123456" }  
The Login page contains a form for existing user authentication.  
By providing an email and password, the app should login a user into the system if there are no empty fields.  
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
Send the following request to perform login:  
Method: POST  
URL: /users/login  
Required headers are described in the documentation. The service expects a body with the following shape:  
{  
  email,  
  password  
}  
Upon success, the REST service will return information about the existing user along with a property accessToken,   
which contains the session token for the user – you need to store this information using sessionStorage or localStorage,  
to be able to perform authenticated requests.  
If the login was successful, redirect the user to the Home page.  
If there is an error, display an appropriate error message, using a system dialog (window.alert).  


### Register User (10 pts)
The Register page contains a form for new user registration.  
By providing an email and password, the app should register a new user in the system if there are no empty fields.   
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
Send the following request to perform registration:  
Method: POST  
URL: /users/register  
Required headers are described in the documentation. The service expects a body with the following shape:  
{  
  email,  
  password  
}  
Upon success, the REST service will return the newly created object with an automatically generated _id and a property accessToken,  
which contains the session token for the user – you need to store this information using sessionStorage or localStorage,  
to be able to perform authenticated requests.  
If the registration was successful, redirect the user to the Home page.   
If there is an error, or the validations don’t pass, display an appropriate error message, using a system dialog (window.alert).  
### Logout (5 pts)
The Logout action is available to logged-in users. Send the following request to perform logout:  
Method: GET  
URL: /users/logout  
Required headers are described in the documentation. Upon success, the REST service will return an empty response.  
Clear any session information you’ve stored in browser storage.  
If the logout was successful, redirect the user to the Home page.  
### Catalog Page (10 pts)
This page displays a list of all albums in the system, with their information.  
All users should be seeing albums, but only logged-in users should see the details button and the Details page.   
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
Clicking on any of the cards details button leads to the details page for the selected album.  
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
If there are no albums, the following view should be displayed:  
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
Send the following request to read the list of albums:  
Method: GET  
URL: /data/albums?sortBy=_createdOn%20desc&distinct=name  
Required headers are described in the documentation. The service will return an array of albums.  

### Home Page (10 pts)
All users should be greeted from the homepage. There is a static page.   
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
### Create Page (15 pts)
The Create page is available to logged-in users.  
It contains a form for creating new albums.  
Check if all the fields are filled before you send the request.    
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
To create an album, send the following request:  
Method: POST  
URL: /data/albums  
Required headers are described in the documentation. The service expects a body with the following shape:  
{  
  name,  
  imgUrl,  
  price,  
  releaseDate,  
  artist,  
  genre,  
  description  
}  
Required headers are described in the documentation. The service will return the newly created record.  
Upon success, redirect the user to the Catalog page.  
### Details (10 pts)
Users should be able to view details about albums.  
Clicking the Details link in of an album should display the Details page.   
If the currently logged-in user is the creator of the album, the Edit and Delete buttons should be displayed.    
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
Send the following request to read a single album:  
Method: GET  
URL: /data/albums/:id  
Where :id is the id of the desired album. Required headers are described in the documentation.  
The service will return a single object.  
### Edit Page (15 pts)
The Edit page is accessible to logged-in users and allows the author to edit their albums.  
Clicking the Edit a specific album link on the details page should display the Edit page.  
It contains a form with input fields for all relevant properties.  
Make sure all fields are filled in before submitting the request.  
The fields must be filled in when the page is first loaded.  
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
To edit an album, send the following request:  
Method: PUT  
URL: /data/albums/:id  
Where :id is the id of the desired game.  
The service expects a body with the following shape:  
{  
  name,  
  imgUrl,  
  price,  
  releaseDate,  
  artist,  
  genre,  
  description  
}  
Required headers are described in the documentation.  
The service will return the modified record.  
Note that PUT requests do not merge properties and will instead replace the entire record.   
Upon success, redirect the user to the Details page.  
### Delete Article (10 pts)
The Delete action is available to logged-in users, for albums they have created.  
When the author clicks on the Delete action on any of their album, a confirmation dialog should be displayed,   
and upon confirming this dialog, the album should be deleted from the system.  
To delete an album, send the following request:  
Method: DELETE  
URL: /data/albums/:id  
Where :id is the id of the desired album. Required headers are described in the documentation.  
The service will return an object, containing the deletion time. Upon success, redirect the user to the Catalog page.  
### (BONUS) Search Page (15 pts)
The Search page allows both users and guests to filter albums by their album's name.  
It contains an input field and, upon submitting a query, a list of all matching albums.   
Check if the field is filled before you send the request. If it isn't filled show an alert message.    
![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
Details button should be visible if the user is logged in.  
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  
   
If there are no results, the following view should be displayed:  
 ![alt text](https://github.com/skyepaper/JavaScript/blob/main/JavaScriptApplication/MusicApp/Pics/Pic%20(1).bmp)  

Send the following request to read a filtered list of albums by their name:  
Method: GET  
URL: /data/albums?where=name%20LIKE%20%22${query}%22  
Where {query} is the search query that the user has entered in the input field.  
Required headers are described in the documentation. The service will return an array of albums.  
