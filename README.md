Following this [tutorial](http://cwbuecheler.com/web/tutorials/2013/node-express-mongo) to set up Node.js with Express, Jade, and MongoDB

Create project  
```bash  
$ express nodetest1  
```  

Enter and Open Project Folder with Sublime Text
```bash  
$ cd nodetest1  
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


//make folder for MongoDB data  
$ mkdir data 
