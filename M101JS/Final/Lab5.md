
```
 this.getCart = function(userId, callback) {
        "use strict";

        /*
        * TODO-lab5
        *
        * LAB #5: Implement the getCart() method.
        *
        * Query the "cart" collection by userId and pass the cart to the
        * callback function.
        *
        */
        this.db.collection("cart").findOne({"userId":userId},function(err,userCart){
             callback(userCart);

        });
       /* var userCart = {
            userId: userId,
            items: []
        }*/
       // var dummyItem = this.createDummyItem();
        //userCart.items.push(dummyItem);

        // TODO-lab5 Replace all code above (in this method).

        // TODO Include the following line in the appropriate
        // place within your code to pass the userCart to the
        // callback.
       
    }
```
