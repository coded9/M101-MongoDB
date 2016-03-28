#Week2

#2.1
```
mongo --shell pcat homework2.js
b = db.products_bak; db.products.find().forEach( function(o){ b.insert(o) } )
 // check it worked: 
b.count()
// should print 11
homework.a()
//3.05
```
#2.2
```
db.products.insert({ "_id" : "ac67", "name" : "AC9 Phone", "brand" : "ACME", "type" : "phone", "price" : 333, "warranty_years" : 0.25, "available" : true })
myobj = db.products.findOne({_id : ObjectId("507d95d5719dbef170f15c00")})
myobj.term_years = 3
db.products.save(myobj)
myobj.limits.sms.over_rate = 0.01
db.products.save(myobj)
homework.b()
//0.050.019031
```
#2.3
```
 db.products.find({"limits.voice" :{$exists:true}}).count()
 //3
 ```
