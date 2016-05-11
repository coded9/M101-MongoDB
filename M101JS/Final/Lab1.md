Final: Lab 1

The items.js file implements data access for the item collection. The item collection contains the product catalog for the MongoMart application.

The mongomart.js application instantiates an item data access object (DAO) with this call:
```
var items = new ItemDAO(db);
```
The DAO, items, is used throughout mongomart.js to implement several of the routes in this application.

In this lab, you will implement the methods in items.js necessary to support the root route or "/". This route is implemented in mongomart.js in the function that begins with this line:
```
router.get("/", function(req, res) {
```
The methods you will implement in items.js are: getCategories(), getItems(), and getNumItems(). The comments in each of these methods describe in detail what you need to do to implement each method. When you believe you are finished, restart the mongomart.js application and evaluate your application to see whether it matches the following description.

If you have completed this lab correctly, the landing page for Mongomart should now show the following five products: Gray Hooded Sweatshirt, Coffee Mug, Stress Ball, Track Jacket, and Women's T-shirt. On the left side of the page you should see nine product categories listed, beginning with "All" and ending with "Umbrellas". At the bottom of the page you should see tabs for pages 1-5 with the statement "23 Products" immediately underneath.

If your application matches the above description, please answer the following question.

Select the "Apparel" category by clicking on it with your mouse. This category contains six products. MongoMart will paginate the products in this category into two pages. Which of the following items is listed on the second page? There should be only one item on this page. Please make sure you are sorting query results as specified in the Lab 1 instructions or you might get the wrong answer.

- [ ] Gray Hooded Sweatshirt
- [ ] Track Jacket
- [ ] Women's T-shirt
- [X] WiredTiger T-shirt
- [ ] Green T-shirt
- [ ] MongoDB University T-shirt

#1A
```
this.getCategories = function(callback) {
        "use strict";
         
        /*
        * TODO-lab1A
        *
        * LAB #1A: Implement the getCategories() method.
        *
        * Write an aggregation query on the "item" collection to return the
        * total number of items in each category. The documents in the array
        * output by your aggregation should contain fields for "_id" and "num".
        *
        * HINT: Test your mongodb query in the shell first before implementing
        * it in JavaScript.
        *
        * In addition to the categories created by your aggregation query,
        * include a document for category "All" in the array of categories
        * passed to the callback. The "All" category should contain the total
        * number of items across all categories as its value for "num". The
        * most efficient way to calculate this value is to iterate through
        * the array of categories produced by your aggregation query, summing
        * counts of items in each category.
        *
        * Ensure categories are organized in alphabetical order before passing
        * to the callback.
        *
        */
        
        
         this.db.collection("item").aggregate([{$group:{_id:"$category",total:{$sum:1}}},
         {$project:{_id:1,num:"$total"}}],
         function(err,result){
          	var categories = [];
         	  var totalItems = 0;
         	  result.forEach(function(category){
         		categories.push(category);
         		totalItems += category.num;
         	});
         	var category = {
            _id: "All",
            num: 9999
        };
        categories.push(category);
        categories.sort(function(a,b){
        	if(a._id < b._id) return -1;
        	if(a._id > b._id) return 1;
        	return 0;
        });
    callback(categories);

      });
        // TODO-lab1A Replace all code above (in this method).
        // TODO Include the following line in the appropriate
        // place within your code to pass the categories array to the
        // callback.
    }
```
#1B
```
this.getItems = function(category, page, itemsPerPage, callback) {
        "use strict";
        var query = { category: category };
        if (category == "All") {
            query = {};
        }

        this.db.collection("item").find(query)
            .sort({ _id: 1 })
            .limit(itemsPerPage)
            .skip((page * itemsPerPage))
            .toArray(function (err, pageItems) {
                assert.equal(null, err);

                callback(pageItems);
            });
        /*
         * TODO-lab1B
         *
         * LAB #1B: Implement the getItems() method.
         *
         * Create a query on the "item" collection to select only the items
         * that should be displayed for a particular page of a given category.
         * The category is passed as a parameter to getItems().
         *
         * Use sort(), skip(), and limit() and the method parameters: page and
         * itemsPerPage to identify the appropriate products to display on each
         * page. Pass these items to the callback function.
         *
         * Sort items in ascending order based on the _id field. You must use
         * this sort to answer the final project questions correctly.
         *
         * Note: Since "All" is not listed as the category for any items,
         * you will need to query the "item" collection differently for "All"
         * than you do for other categories.
         *
         */

        /*var pageItem = this.createDummyItem();
        var pageItems = [];
        for (var i=0; i<5; i++) {
            pageItems.push(pageItem);
        }*/

        // TODO-lab1B Replace all code above (in this method).

        // TODO Include the following line in the appropriate
        // place within your code to pass the items for the selected page
        // to the callback.
       
    }
```
#1C
```
this.getNumItems = function(category, callback) {
        "use strict";

        var numItems = 0;
     //  numItems = category.num;
        /*
         * TODO-lab1C:
         *
         * LAB #1C: Implement the getNumItems method()
         *
         * Write a query that determines the number of items in a category
         * and pass the count to the callback function. The count is used in
         * the mongomart application for pagination. The category is passed
         * as a parameter to this method.
         *
         * See the route handler for the root path (i.e. "/") for an example
         * of a call to the getNumItems() method.
         *
         */
         var query = { category: category };
        if (category == "All") {
            query = {};
        }

        this.db.collection("item").count(
            query,
            function (err, numItems) {
                assert.equal(null, err);

                callback(numItems);
            });


         // TODO Include the following line in the appropriate
         // place within your code to pass the count to the callback.
     //   callback(numItems);
    }
```    
