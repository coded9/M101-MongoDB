Final: Lab 2

In this lab, you will implement the methods in items.js necessary to support the route for text search or "/search". This route is implemented in mongomart.js in the function that begins with this line:
```
router.get("/search", function(req, res) {
```
The methods you will implement in items.js are: searchItems(), and getNumSearchItems(). The comments in each of these methods describe in detail what you need to do to implement each method. When you are finished, restart the mongomart.js application and answer the question below.

How many products match the query, "leaf"?
//Ans:7

#2A
```
this.searchItems = function(query, page, itemsPerPage, callback) {
        "use strict";
     this.db.collection("item").find({$text:{$search:query}})
         .sort({_id:1}).limit(itemsPerPage)
         .skip((page * itemsPerPage))
         .toArray(function(err,items){
         	assert.equal(null,err);
         	callback(items);
         });
        /*
         * TODO-lab2A
         *
         * LAB #2A: Implement searchItems()
         *
         * Using the value of the query parameter passed to searchItems(),
         * perform a text search against the "item" collection.
         *
         * Sort the results in ascending order based on the _id field.
         *
         * Select only the items that should be displayed for a particular
         * page. For example, on the first page, only the first itemsPerPage
         * matching the query should be displayed.
         *
         * Use limit() and skip() and the method parameters: page and
         * itemsPerPage to select the appropriate matching products. Pass these
         * items to the callback function.
         *
         * searchItems() depends on a text index. Before implementing
         * this method, create a SINGLE text index on title, slogan, and
         * description. You should simply do this in the mongo shell.
         *
         */

       /* var item = this.createDummyItem();
        var items = [];
        for (var i=0; i<5; i++) {
            items.push(item);
        }*/

        // TODO-lab2A Replace all code above (in this method).

        // TODO Include the following line in the appropriate
        // place within your code to pass the items for the selected page
        // of search results to the callback.
    }
```
#2B
```
this.getNumSearchItems = function(query, callback) {
        "use strict";

        var numItems = 0;
       this.db.collection("item").count({$text:{$search:query}},function(err,numItems){
       	assert.equal(null,err);
       	callback(numItems);
       })
        /*
        * TODO-lab2B
        *
        * LAB #2B: Using the value of the query parameter passed to this
        * method, count the number of items in the "item" collection matching
        * a text search. Pass the count to the callback function.
        *
        * getNumSearchItems() depends on the same text index as searchItems().
        * Before implementing this method, ensure that you've already created
        * a SINGLE text index on title, slogan, and description. You should
        * simply do this in the mongo shell.
        */

        
    }
```
Finally create the index and click the button
```
>db.item.createIndex({title:'text',description:'text',slogan:'text'})
```
