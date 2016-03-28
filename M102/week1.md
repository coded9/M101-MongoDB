#Week1

#1.1
```
db.isMaster().maxBsonObjectSize
16777216
```
#1.2
```
mongoimport --db pcat --collection products --file products.json
db.products.find( { type : "case" } ).count()
3
```
#1.3
```
db.products.find({brand:"ACME"})
```
#1.4
```
var c = db.products.find( { }, { name : 1, _id : 0 } ).sort( { name : 1 } ); while( c.hasNext() ) { print( c.next().name); }
var c = db.products.find( { } ).sort( { name : 1 } ); c.forEach( function( doc ) { print( doc.name ) } );
```
