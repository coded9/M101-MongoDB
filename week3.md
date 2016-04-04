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

//Did this assignment in cloud9 IDE so 0.0.0.0 instead of localhost
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
#3.3
```
function queryDocument(options) {

    console.log(options);
    
    var query = {
        "tag_list":{"$regex":"social-networking" }/* TODO: Complete this statement to match the regular expression "social-networking" */        
    };

    if (("firstYear" in options) && ("lastYear" in options)) {
      query.founded_year = {
            "$gte": options.firstYear,
           "$lte": options.lastYear
        };
       /* query['$and'] = [ {'founded_year': { "$gte": options.firstYear }}, {'founded_year': { "$lte": options.lastYear }} ]*/
        
        /* 
           TODO: Write one line of code to ensure that if both firstYear and lastYear 
           appear in the options object, we will match documents that have a value for 
           the "founded_year" field of companies documents in the correct range. 
        */
    } else if ("firstYear" in options) {
        query.founded_year = { "$gte": options.firstYear };
    } else if ("lastYear" in options) {
        query.founded_year = { "$lte": options.lastYear };
    }

    if ("city" in options) {
        query["offices.city"] = options.city;
        /* 
           TODO: Write one line of code to ensure that we do an equality match on the 
           "offices.city" field. The "offices" field stores an array in which each element 
           is a nested document containing fields that describe a corporate office. Each office
           document contains a "city" field. A company may have multiple corporate offices. 
        */
    }
        
    return query;
    
}
```
```
{ firstYear: 2002, lastYear: 2016, city: 'Palo Alto' }
{ lastYear: 2010, city: 'New York' }
{ city: 'London' }
Successfully connected to MongoDB for query: 0
Successfully connected to MongoDB for query: 1
Successfully connected to MongoDB for query: 2
Query 0 was:{"tag_list":{"$regex":"social-networking"},"founded_year":{"$gte":2002,"$lte":2016},"offices.city":"Palo Alto"}
Matching documents: 6
Query 1 was:{"tag_list":{"$regex":"social-networking"},"founded_year":{"$lte":2010},"offices.city":"New York"}
Matching documents: 20
Query 2 was:{"tag_list":{"$regex":"social-networking"},"offices.city":"London"}
Matching documents: 20
Companies found: asmallworld,bookglutton,buongiorno,buzzr,bview,doostang,event-innovation,facebook,fledgewing,flirtomatic,fotolog,getitwithme,gocrosscampus,hellotxt,innerrewards,instablogs,ipadio,justmeans,mangoapps,mobikade,mystylepost,omnivents,people-capital,publictivity,recommend-box,selectminds,sendible,skydeck,social-sauce,socialgo,socialtext,talkbiznow,tradingup-online,trustedplaces,unltdworld,unype,weardrobe,webjam,yammer,yellowspaces,zedge,zemoga
Total employees in companies identified: 7130
Total unique companies: 42
Average number of employees per company: 169
```
