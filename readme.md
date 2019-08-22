# This starter is usefull when we need to create headless server with the help of Node.js ,MongoDB(mongodb-driver)

download repo or clone it 
1. cmd :npm install 
2. cmd : node server.js  > to run server 

##  MongoDb with mongodb driver 
### MongoDB driver : https://docs.mongodb.com/manual/reference/operator/ 
#### this project is based on mongodb driver so we need to install : cmd : npm install mongodb@2.2.33 --save

  
# Demo server.js : Sample Formate of Examples
 
const { MongoClient } = require('mongodb');
 
const url = 'mongodb://localhost:27017/test';
 
MongoClient.connect(url,(err,db)=>{

   if(err){
       console.log('could not connected.');
   }
   console.log('connection successfully');

   db.collection('Cars').insertOne({
       model : 'Ford',
       year : 2019
   },(err,res)=>{
       if(err){
           return console.log(`we get error : ${err}`)
       }
       console.log(res.ops[0]._id.getTimestamp());
   })
 
   db.close();
})

## database is connected or not

    MongoClient.connect(url,(err,db)=>{
        if(err){
            console.log('could not connected.');
        }
        console.log('connection successfully');

##  Example 1 : Add data in database
### 1.1 insertOne() : add one collection using insertOne Method 
        db.collection('Cars').insertOne({
            model : 'Ford',
            year : 2019
        },(err,res)=>{ 
            if(err){
                return console.log(`we get error : ${err}`)
            }
            console.log(res.ops[0]._id.getTimestamp());
        }) 

        db.close();

### 1.2 insert() : add multiple data in database 
        let cars = [
            {model : 'Ford' , year : 2019},
            {model : 'Oddi' , year : 2019}
        ]
        db.collection('Cars').insert(cars,(err,res)=>{ // insted of cars > single we can store {model : 'Oddi' , year : 2019} 
            if(err){
                return console.log(`we get error : ${err}`)
            }
            console.log(res.ops);
        }) 
        db.close(); 
### 1.3 insertMany() : we can only insert multiple recoreds 
       let cars = [
            {model : 'Ford' , year : 2019},
            {model : 'Oddi' , year : 2019}
        ]
        db.collection('Cars').insertMany(cars,(err,res)=>{ //we can't insert single value using insertMany
            if(err){
                return console.log(`we get error : ${err}`)
            }
            console.log(res.ops);
        }) 
        db.close();
       
## Example 2: how to get or find data from mongodb
### 2.1 : find() gives all data 
      db.collection('Cars').find().toArray().then(data=>{
          console.log(data);
      }) 
      db.close();

### 2.2 : skip() we can skip the data in find()
    
     db.collection('Cars').find().skip(1).toArray().then(data=>{
        console.log(data);
    }) 
    db.close();
    
### 2.3 : limit() we can give limit to find()
   
    db.collection('Cars').find().limit(2).toArray().then(data=>{
    console.log(data);
    }) 
    db.close();
   
### 2.4 : sort() we can sort our data
    
   db.collection('Cars').find()
    .sort({"_id" : -1})
    .toArray().then(data=>{
        console.log(data);
    }) 
    db.close(); 
   
### 2.5 : find using key or value - it gives all the records which match the condition
    db.collection('Cars').find({model:"Oddi"}).toArray().then(data=>{
        console.log(data);
    }) 
    db.close();
   
### 2.6 : findOne using key or value - it gives only first-one record which match the condition
    db.collection('Cars').findOne({model:"Oddi"},(err,doc)=>{
        console.log(doc)
    })
    db.close();
        
### 2.7 : findOne we can skip perticuler colums using second object in findOne()
    db.collection('Cars').findOne({model:"Oddi"},{model:0,year:0},(err,doc)=>{
        console.log(doc)
    })
    db.close();
  
##  Example 3 : delete data
### 3.1 deleteMany() : delete data from collection which setisfy the condition 
      db.collection('Cars').deleteMany({ year :2019},(err,doc)=>{
            console.log(doc);
        })
        db.close();
     

### 3.2 deleteOne() : delete only first one data from collection which setisfy the condition 
      db.collection('Cars').deleteOne({ year :2019},(err,doc)=>{
            console.log(doc);
        })
        db.close();
     
### 3.3 findOneAndDelete() : it find one record and delete that 
      db.collection('Cars').findOneAndDelete({ year :2019},(err,doc)=>{
            console.log(doc);
        })
        db.close();
     
## Example 4 : update data 
### 4.1 update one record : create new collection users with name,lastname and age 
     db.collection('Users').findOneAndUpdate(
            {
                name : "prakash"
            },
            {
                $set : {
                    lastname : "karena"
                }
            },
            {
                returnOriginal : false
            },
            (err,doc)=>{
                console.log(doc)
            }
       )
       
      db.close(); 

### 4.2 update one record if not exist then add it 
      db.collection('Users').findOneAndUpdate(
            {
                name : "ravi"
            },
            {
                $set : {
                    lastname : "chavda"
                }
            },
            {
                upsert : true ,
                returnOriginal : false
            },
            (err,doc)=>{
                console.log(doc)
            }
       )
       
      db.close(); 
### 4.3 update one record and increment age by 2  
     db.collection('Users').findOneAndUpdate(
            {
                name : "ravi"
            },
            {
                $set : {
                    lastname : "karena"
                }
                ,
                $inc : {
                    age : +2
                }
            },
            {
                upsert : true ,
                returnOriginal : false
            },
            (err,doc)=>{
                console.log(doc)
            }
       )
      db.close(); 

    })
    


