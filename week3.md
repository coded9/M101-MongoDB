#Week3

#3.1
```
When using find() in the Node.js driver, which of the following best describes when the driver will send a query to MongoDB?
Ans:When we call a cursor method passing a callback function to process query results
```
#3.2
```
var MongoClient = require('mongodb').MongoClient,
    assert = require('assert');


MongoClient.connect('mongodb://0.0.0.0:27017/school', function(err, db) {

    assert.equal(err, null);
    console.log("Successfully connected to MongoDB.");

    
var cursor = db.collection("grades").find({});
cursor.skip(6);
cursor.limit(2);
cursor.sort({"grade": 1});
cursor.toArray(function(err, docs) {

        assert.equal(err, null);
        assert.notEqual(docs.length, 0);
        
        docs.forEach(function(doc) {
            console.log(doc);
        });
        
        db.close();
        
    });
});
```
