Following this [tutorial](http://cwbuecheler.com/web/tutorials/2013/node-express-mongo) to set up Node.js with Express, Jade, and MongoDB

Create project  
```bash  
$ express projectname  
```  

Enter and Open Project Folder with Sublime Text
```bash  
$ cd projectname  
$ subl .  
```  

Add Dependencies in 'package.json'  

Install Dependencies
```bash  
$ npm install  
``` 
Start server with nodemon for auto restarts
```bash  
$ cd bin  
$ nodemon www  
```  

View webpage  
[http://localhost:3000](http://localhost:3000)

Create route to helloword in index.js  
```javascript
router.get('/helloworld', function(req, res) {
    res.render('helloworld', { title: 'Hello, World!' })
});
```

Create helloworld page  
Open index.jade and save as helloworld.jade  
Change to match the following:
```jade
extends layout

block content
    h1= title
    p Hello, World! Welcome to #{title}
```


View helloworld webpage  
[http://localhost:3000/helloworld](http://localhost:3000/helloworld)

Install MongoDB from the [official website](http://www.mongodb.org/downloads)

Extract File and Move
```bash  
$ cd ~/Download
$ tar xzf mongodb-osx-x86_64-2.2.3.tgz
$ sudo mv mongodb-osx-x86_64-2.2.3 /usr/local/mongodb
```  

Add MongoDB to PATH variable in bash_profile
```
$ open ~/.bash_profile
//copy & paste the below to bash_profile
export MONGO_PATH=/usr/local/mongodb
export PATH=$PATH:$MONGO_PATH/bin
$ source ~/.bash_profile
```

Set DB path and start MongoDB server
```bash
$ cd projectname
$ mkdir data
$ mongod --dbpath data
```  

Insert Data
```bash
$ mongo
MongoDB shell version: 2.6.5
connecting to: test
> use projectname
switched to db projectname
> db.usercollection.insert({ "username" : "testuser1", "email" : "testuser1@testdomain.com" })
> db.usercollection.find().pretty()
> newstuff = [{ "username" : "testuser2", "email" : "testuser2@testdomain.com" }, { "username" : "testuser3", "email" : "testuser3@testdomain.com" }]
> db.usercollection.insert(newstuff);
```

Let the app.js know we're using MongoDB through Monk, and our database is located at localhost:27017/projectname. 
```javascript
var mongo = require('mongodb');
var monk = require('monk');
var db = monk('localhost:27017/projectname');
```
Let router access db
```javascript
// add before app.use('/', routes);
app.use(function(req,res,next){
    req.db = db;
    next();
});
```
Add userlist route to index.js  
Let the app know we want to use ('usercollection')  
Find and return the results as a variable: "docs"  
```javascript
/* GET Userlist page. */
router.get('/userlist', function(req, res) {
    var db = req.db;
    var collection = db.get('usercollection');
    collection.find({},{},function(e,docs){
        res.render('userlist', {
            "userlist" : docs
        });
    });
});
```

Add userlist webpage  
Open index.jade and save as userlist.jade  
Change to match the following:  
```jade
extends layout

block content
    h1.
        User List
    ul
        each user, i in userlist
            li
                a(href="mailto:#{user.email}")= user.username
```

Checkout userlist webpage  
[http://localhost:3000/userlist](http://localhost:3000/userlist)
