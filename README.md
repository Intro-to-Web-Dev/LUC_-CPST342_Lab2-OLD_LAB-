#  Nodejs Express App - Create and Retrieve Users (Lab 2)
You are going to build a web application that allows end-users to create user profiles and view all profiles created.  This lab focuses on using Nodejs as the back-end server language and implementing core modules (File System core module), third-party modules (Express Framework), user-defined modules (User Object).  

## Requirements

### Step 1 - Create a web project and implement version control
1.  Create a folder titled **[lab2]**
2.  Make sure you are in the newly created directory and install git by running command **[git init]**
3.  Execute a git command to pull down the README.md file that contains lab instructions **Make sure your local branch name aligns with your remote branch name before pulling contents down - before pulling contents down run the command git branch -M main**]
4.  Create a .gitignore file and add **[node_modules]** to the file.

### Step 2 - Configure and install Express
1.  Run command **[npx express-generator --view hbs]**
	1.  This command scaffolds the application with a folder structure and the --view hbs sets the view template to handlebars.js
    2.  Refer to http://expressjs.com/en/starter/generator.html to understand other configuration options
	3.  Install dependencies listed in package.json by running command [npm install]
	4.  Fix any dependencies by running command [npm audit fix]
2.  Run command **[npm start]** and view application in browser by navigating to localhost:3000.  
3.  After viewing application in browser stop application by running **[Control + C]**
	
### Step 3 - Understand the  statements in App.js and project folder structure
1.  Understand the folder structure
	1.  The public folder contains static resources such as css, images, etc.  This statement [app.use(express.static(path.join(__dirname, 'public')));] in app.js is what allows you to reference items.
	2.  The views folder contains all of your applications various rendered html.  The statements [app.set('views', path.join(__dirname, 'views'));  app.set('view engine', 'hbs');] in app.js is what allows you to set the template engine to handlebars.js and reference the folder.
		1.  Within the views folder create three views **[createuser.hbs]** , **[users.hbs]** and **[display.hbs]**
	3.  The routes folder have files that contain functions that get involked when a user enters a desired path in the browser.  The statements	[var indexRouter = require('./routes/index');  var usersRouter = require('./routes/users');] in app.js make the middleware functions available to app.js.  The statements [app.use('/', indexRouter);  app.use('/users', usersRouter);] allow are application to use the defined routes.
		1.  Within the routes folder create a two route file **[createuser.js]** and **[adduser.js]** and copy the contents of user.js into each new file.
		2.  Add routes under current routes to app.js file **[var createUserRouter = require('./routes/createuser'); var addUserRouter = require('./routes/adduser');**
		3.  Include statements to use the various routes defined in route files.  **[app.use('/create', createUserRouter);  app.use('/adduser', addUserRouter);]**
	4.  Create a folder called "model" and create a new file within the model folder and name it **[user.js]**
### Step 4 - Implement Business (Model) Logic
1.  **Business (Model) Logic** - What are attributes and behavior that each user need to have?  
	1. Each user will have a first name, last name, email and password.
	2. Implement the logic below into user.js file that is in the model folder:
		```javascript
		var user = {

			firstName: "",
			lastName: "",
			email: "",
			password: ""

		}

		exports.user;
		```
		
### Step 5 - Display (View) Logic - Adding HTML and CSS to the application and make sure to save each file after alteration.
1.  Navigate to the **[createuser.hbs]** file within the view folder and paste the html code below:
	```html
	<h1>User Entry Form:</h1>
	<form action="/adduser" method="POST">
		<input type="text"  name="fname" class="form-control" placeholder="Enter First name (ex. Noah)" size="40"><br>
		<input type="text"  name="lname" class="form-control" placeholder="Enter Last Name (ex. Smith)" size="40"><br>
		<input type="email"  name="email" class="form-control" placeholder="Enter Email (ex. Nsmith@example.com)" size="40"><br>
		<input type="password" class="form-control" name="password" placeholder="Enter password" size="40"><br>
		<input type="submit" class="btn btn-primary" value="submit">
	</form>
	```
	
2.  Navigate to the **[display.hbs]** file within the view folder and paste the html code below:
	```html
	<div>
		<h1>Created User:</h1>
		<p>First Name: {{firstName}}</p>
		<p>Last Name: {{lastName}}</p> 
		<p>Email: {{email}} </p> 
		<p>Password: {{password}}</p>
	</div>
	<a href="/users"><button type="button" class="btn btn-success">View All Users</button></a>
	```
3.  Navigate to the **[users.hbs]** file within the view folder and paste the html code below:
	```html
	<h1>List of site users:</h1>
	<table>
			<tr>
				<th>First Name</th>
				<th>Last Name</th>
				<th>Email</th>
			</tr>
		{{#each createdUsers}}
			<tr>
				<td>{{this.firstName}}</td>
				<td>{{this.lastName}}</td>
				<td>{{this.email}}</td>
			</tr>
		{{/each}}
	</table>
	```
4.  Navigate to the **[index.hbs]** file within the view folder and paste the html code below:
	```html
	<h1>{{title}}</h1>
	<p>Welcome to {{title}}</p>
	<p>This node application walks through the basic's of routing, read and writing to json file, templating with handlebars.js and passing data to and from the back-end. </p>
	<p>Please use the paths below to navigate application</p>
	<ul>
		<li><span style="font-weight: 700;">Home Page</span> - /</li>
		<li><span style="font-weight: 700;">Create a User</span> - /create</li>
		<li><span style="font-weight: 700;">Display all Users</span> - /users</li>
	</ul>
	```
5.  Navigate to the **[layout.hbs]** file within the view folder and past the CDN Bootstrap link within the head element under the current css link:
	```html
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
	```
6.  Navigate to the **[style.css]** file within the public/stylesheet folder and paste the css code below:
	```css
	table {
	  font-family: arial, sans-serif;
	  border-collapse: collapse;
	  width: 100%;
	}

	td, th {
	  border: 1px solid #dddddd;
	  text-align: left;
	  padding: 8px;
	}

	tr:nth-child(even) {
	  background-color: #dddddd;
	}
	```
### Step 6 - **Application (Controller) Logic** - Applying logic that triggers when an event is triggered or file path is entered
1.  Within the root directory of your project folder, create a file called **[users.json]** and add the square brackets listed below.  **Be careful not to confuse user.js with users.json**
	```javascript
	[]
	```

2.  Navigate to the **[user.js]** file within the route folder and add the require method to make functionality for file system available.
	```javascript
	var fs = require('fs');
	```
	Within the same file, add the following code within the router function that allows you to read the users.json file and convert the string array into an array of js objects.
	```javascipt
	  let userData = fs.readFileSync('./users.json');
	  var siteUsers = JSON.parse(userData);

	  //Assigning the parsed array of objects read-in from users.json to a variable called createdUsers
	  var createdUsers = siteUsers;
	  res.render('users', {createdUsers});
	```

3.  Navigate to the **[adduser.js]** file within the route folder and add the require method to make functionality for file system available and add a require method to bring in the users.json file.
	```javascript
	var fs = require('fs');
	var user = require('../model/user.js');
	```	
	Within the same file, add the following code and delete the current route and add the following post route.  This route creates a user object from our model, reads in the previous array of objects contained within the users.json file, adds our new object and writes the modified array of users objects to the users.json file
	```javascript
	/* Create User */
	router.post('/', function(req, res, next) {

	  //Using the data model user from user.js
	  user.firstName = req.body.fname;
	  user.lastName = req.body.lname;
	  user.email = req.body.email;
	  user.password = req.body.password;

	  //outputting user to console to verify that user was created
	  console.log(user);

	  //reading users from user.json file and assigning user to userData variable
	  let userData = fs.readFileSync('./users.json');

	  //The JSON.parse() is converting the string to JS objects
	  let siteUsers = JSON.parse(userData);

	  //Adding the new user to the end of the converted array that was just read in from users.json
	  siteUsers.push(user);

	  /**Now that the user has been added to the array, the JSON.stringify() method converts the JS array
	  * into a string so that we can override the users.json file and write the updated array of objects to users.json file
	  **/ 
	  const userString = JSON.stringify(siteUsers)
	  fs.writeFile('./users.json', userString, err => {
		  //error handling if, issue arrises with file, else output to successfully wrote file
		  if (err) {
			  console.log('Error writing file', err)
		  } else {
			  console.log('Successfully wrote file')
		  }
	  })

	  //Render the new user object to display view
	  res.render('display', user)
	});
	```
4.  Navigate to the **[createuser.js]** file within the route folder and replace the res.render() function in the route with code below:
	```javascript
	//the statement below contains a render function - the first argument is the view name and the second argument is an object with one key/value pair.
	res.render('createuser', { title: 'Create Account'})
	```
### Step 7 - End-user Interaction
1.  Start the server by running command **[npm start]**
2.  Navigate to localhost:3000 in your browser and add 3 new users and view the users by navigating to the various paths listed on the homepage.
3.  Kill Server by running command **[CTRL + C]**
4.  Run the various workflow commands to make a commit history and push up your files to the remote repository.


### STEP 8 - Extra Credit (3 Points) 
1.  Create a new functionality that would allow you to delete and update an existing user.  This will require you to to implement looping, decision making logic and will require new routes and http verbs such as delete and put.

### STEP 9 - Github Repository
1.  Add Instructor as a contributor to repository by searching for **[instructorc]**
2.  Adjust README.md file at the end to include date of completion and course information.

### STEP 10 - Submission
1.  Comment your name to the app.js file and 
2.  Make sure your master branch is clean and push up your final changes.
3.  In Sakai, submit the URL to your repository
