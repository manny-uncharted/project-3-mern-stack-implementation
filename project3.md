# SIMPLE TO-DO APPLICATION ON MERN WEB STACK

In this project we would be implementing a simple to-do application on MERN stack on an AWS EC2 instance. And we would be performing the following functions:
- backend configuration
- Install expressjs
- Models
- Mongodb database
- frontend creation
- Frontend creation (continued)

## Backend Configuration
Here we would begin by configuring the backend for our to-do app.

- update ubuntu on the instance.
    ```
    sudo apt update
    ```

    Results:
    ![Update the linux server with the latest version of the software.](./img/sudo-apt-update.png)

- upgrade ubuntu on the instance
    ```
    sudo apt upgrade
    ```

    Results:
    ![Upgrade the linux server with the latest version of the software.](./img/sudo-apt-upgrade.png)

- Get the location of Node.js software from Ubuntu repositories.
    ```
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
    ```

    Results:
    ![Install Node.js software from Ubuntu repositories.](./img/get-node-software.png)

- Installing Node.js on the server
    ```
    sudo apt install nodejs
    ```

    Results:
    ![Install Node.js on the server.](./img/sudo-apt-get-install-nodejs.png)

    Note: The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

- verify node installation
    ```
    node -v
    ```

    Results:
    ![Verify node installation.](./img/node-verify.png)

    Note: The command above verifies that nodejs is installed on the server.

- verify npm installation
    ```
    npm -v
    ```

    Results:
    ![Verify npm installation.](./img/npm-verify.png)

    Note: The command above verifies that npm is installed on the server.

- Application Code Setup
    We would need to create a new directory for our To-Do project:

    ```
    mkdir Todo
    ```

    Results:
    ![Create a new directory for our To-Do project.](./img/mkdir-todo.png)

- Run the command below to verify that the Todo directory is created with ls command
    ```
    ls
    ```

    Results:
    ![Verify that the Todo directory is created with ls command.](./img/ls-todo.png)

    Note: The command above verifies that the Todo directory is created with ls command.

- Now we change our current directory to the newly created one
    ```
    cd Todo
    ```

    Results:
    ![Now we change our current directory to the newly created one.](./img/cd-todo.png)

- Next, we will use the command npm init to initialise our project, so that a new file named package.json will be created. This file will normally contain information about our application and the dependencies that it needs to run. Follow the prompts after running the command. We would press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

    ```
    npm init
    ```

    Results:
    ![Next, we will use the command npm init to initialise our project, so that a new file named package.json will be created. This file will normally contain information about our application and the dependencies that it needs to run. Follow the prompts after running the command. We would press Enter several times to accept default values, then accept to write out the package.json file by typing yes.](./img/npm-init.png)

    Note: The command above initialises our project.


## Install ExpressJS
Now we would move on with installing express js.

- To use express, install it using npm.
    ```
    npm install express
    ```

    Results:
    ![To use express, install it using npm.](./img/npm-install-express.png)

    Note: The command above installs expressjs.

- Now create a file index.js with the command below.
    ```
    touch index.js
    ```

    Results:
    ![Now create a file index.js with the command below.](./img/touch-index-js.png)

    Note: The command above creates a file index.js and run ls to confirm that your index.js file is successfully created

- Install the dotenv module
    ```
    npm install dotenv
    ```

    Results:
    ![Install the dotenv module.](./img/npm-install-dotenv.png)

    Note: The command above installs the dotenv module.

- Open the index.js file with the command below.
    ```
    vim index.js
    ```
    and paste the following code:
    ```
    const express = require('express');
    require('dotenv').config();

    const app = express();

    const port = process.env.PORT || 8000;

    app.use((req, res, next) => {
    res.header("Access-Control-Allow-Origin", "\*");
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    next();
    });

    app.use((req, res, next) => {
    res.send('Welcome to Express');
    });

    app.listen(port, () => {
    console.log(`Server running on port ${port}`)
    });
    ```

    Results:
    ![Open the index.js file with the command below.](./img/vim-index-js.png)

    Note: The command above opens the index.js file.

- Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type the following command:
    ```
    node index.js
    ```

    Results:
    ![Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type the following command:](./img/node-index-js.png)

    Note: The command above starts our server.

- Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 8000
    ```
    http://<ip-address>:8000
    ```

    Results:
    ![Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 8000](./img/http-ipaddress-8000.png)

    Note: The command above opens up your browser and try to access your server’s Public IP or Public DNS name followed by port 8000.

### Routes
There are three actions that our To-Do application needs to be able to do:

Create a new task
Display list of all tasks
Delete a completed task
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

- For each task, we need to create routes that will define various endpoints that the To-do app will depend on. 

    So let us create a folder routes and change directory to the routes folder
    ```
    mkdir routes
    cd routes
    ```

    Results:
    ![For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes.](./img/mkdir-routes.png)

    Note: The command above creates a folder routes and helps us change directory into that created folder.

- Now, create a file api.js with the command below.
    ```
    touch api.js
    ```

    Results:
    ![Now, create a file api.js with the command below.](./img/touch-api-js.png)

    Note: The command above creates a file api.js and run ls to confirm that your api.js file is successfully created

- Open the file with the command below
    ```
    nano api.js
    ```
    and paste the following code:
    ```
    const express = require ('express');
    const router = express.Router();

    router.get('/todos', (req, res, next) => {

    });

    router.post('/todos', (req, res, next) => {

    });

    router.delete('/todos/:id', (req, res, next) => {

    })

    module.exports = router;
    ```

    Results:
    ![Open the file with the command below.](./img/nano-api-js.png)

    Note: The command above opens the file api.js and allows us to enter the commands and create the get, delete and post endpoints.

## Models
Moving forward let's create Models directory.

Since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document
In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

- To use mongoose, install it using npm.
    ```
    npm install mongoose
    ```

    Results:
    ![To use mongoose, install it using npm.](./img/npm-install-mongoose.png)

    Note: The command above installs mongoose.

- Create a new folder models and change directory into the newly created models folder.
    ```
    mkdir models
    cd models
    ```

    Results:
    ![Create a new folder models and change directory into the newly created models folder.](./img/mkdir-models.png)

    Note: The command above creates a folder models and helps us change directory into that created folder.

- Inside the models folder, create a file and name it todo.js
    ```
    touch todo.js
    ```

    Results:
    ![Inside the models folder, create a file and name it todo.js](./img/touch-todo-js.png)

    Note: The command above creates a file todo.js and run ls to confirm that your todo.js file is successfully created

- Open the file created with vim todo.js then paste the code below in the file
    ```
    const mongoose = require('mongoose');
    const Schema = mongoose.Schema;

    //create schema for todo
    const TodoSchema = new Schema({
    action: {
    type: String,
    required: [true, 'The todo text field is required']
    }
    })

    //create model for todo
    const Todo = mongoose.model('todo', TodoSchema);

    module.exports = Todo;
    ```

    Results:
    ![Open the file created with vim todo.js then paste the code below in the file](./img/nano-todo-js.png)

    Note: The command above opens the file todo.js and then you paste the code below in the file.

- Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

    In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit

    ```
    const express = require ('express');
    const router = express.Router();
    const Todo = require('../models/todo');

    router.get('/todos', (req, res, next) => {

    //this will return all the data, exposing only the id and action field to the client
    Todo.find({}, 'action')
    .then(data => res.json(data))
    .catch(next)
    });

    router.post('/todos', (req, res, next) => {
    if(req.body.action){
    Todo.create(req.body)
    .then(data => res.json(data))
    .catch(next)
    }else {
    res.json({
    error: "The input field is empty"
    })
    }
    });

    router.delete('/todos/:id', (req, res, next) => {
    Todo.findOneAndDelete({"_id": req.params.id})
    .then(data => res.json(data))
    .catch(next)
    })

    module.exports = router;
    ```

    Results:
    ![Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.](./img/nano-upd-api-js.png)


## MONGODB Database
MongoDB Database
We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up here. Follow the sign up process, select AWS as the cloud provider, and choose a region near you.

- create an account and complete the checklist
    - Create a MongoDB database and collection inside mLab
    - Allow access to the MongoDB database from anywhere (Not secure, but it is ideal for testing)
    
    Results:
    ![Mongodb setup](./img/create-account.png)

In the index.js file, we specified process.env to access environment variables, but we have not yet created this file. So we need to do that now.

- we would create a file in our Todo directory and name it .env.
    ```
    touch .env
    nano .env
    ```
    And add the connection string to access the database in it, just as below:
    ```
    DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
    ```
    ```Ensure to update <username>, <password>, <network-address> and <database> according to your setup```

    Results:
    ![we would create a file in our Todo directory and name it .env.](./img/touch-env.png)

    Note: The command above creates a file .env and run ls to confirm that your .env file is successfully created.

- Now we need to update the index.js to reflect the use of .env so that Node.js can connect to the database.
    ```
    const express = require('express');
    const bodyParser = require('body-parser');
    const mongoose = require('mongoose');
    const routes = require('./routes/api');
    const path = require('path');
    require('dotenv').config();

    const app = express();

    const port = process.env.PORT || 5000;

    //connect to the database
    mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log(`Database connected successfully`))
    .catch(err => console.log(err));

    //since mongoose promise is depreciated, we overide it with node's promise
    mongoose.Promise = global.Promise;

    app.use((req, res, next) => {
    res.header("Access-Control-Allow-Origin", "\*");
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    next();
    });

    app.use(bodyParser.json());

    app.use('/api', routes);

    app.use((err, req, res, next) => {
    console.log(err);
    next();
    });

    app.listen(port, () => {
    console.log(`Server running on port ${port}`)
    });
    ```

    Results:
    ![Now we need to update the index.js to reflect the use of .env so that Node.js can connect to the database.](./img/nano-index-js.png)

