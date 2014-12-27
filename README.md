Following this [tutorial](http://cwbuecheler.com/web/tutorials/2013/node-express-mongo) to set up Node.js with Express, Jade, and MongoDB

Create project  
```bash  
$ express nodetest1  
```  

Enter and Open Project Folder with Sublime Text
```bash  
$ cd projectfolder  
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
View webpage  
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
$ cd projectfolder
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
