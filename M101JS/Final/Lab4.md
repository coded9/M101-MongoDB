```
this.addReview = function(itemId, comment, name, stars, callback) {
        "use strict";

        /*
         * TODO-lab4
         *
         * LAB #4: Implement addReview().
         *
         * Using the itemId parameter, update the appropriate document in the
         * "item" collection with a new review. Reviews are stored as an
         * array value for the key "reviews". Each review has the fields:
         * "name", "comment", "stars", and "date".
         *
         */
        
        	
        var reviewDoc = {
            name: name,
            comment: comment,
            stars: stars,
            date: Date.now()
        }	
        this.db.collection("item").updateOne({_id:itemId},{$push:{"reviews":reviewDoc}},function(err,doc){
                assert.equal(null,err);
        
        
        callback(doc);
        });
        

        // TODO replace the following two lines with your code that will
        // update the document with a new review.
        //var doc = this.createDummyItem();
        //doc.reviews = [reviewDoc];

        // TODO Include the following line in the appropriate
        // place within your code to pass the updated doc to the
        // callback.
        
    }

```
