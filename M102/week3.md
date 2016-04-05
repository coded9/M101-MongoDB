#3.3
```
Create an index on the products collection for the field, "for".

After creating the index, do a find() for products that work with an "ac3" phone ("ac3" is present in the "for" field).

Q1: How many products match this query?
Q2: Run the same query, but this time do an explain(). How many documents were examined?
Q3: Does the explain() output indicate that an index was used?
```
```
Answer:
db.products.createIndex({for:1})
Q1:db.products.find({for:"ac3"}).count()
Q2,Q3: db.products.explain("executionStats").find({for:"ac3"})
Observe the output highlighted below
```
 db.products.explain("executionStats").find({for:"ac3"})
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "pcat.products",
                "indexFilterSet" : false,
                "parsedQuery" : {
                        "for" : {
                                "$eq" : "ac3"
                        }
                },
                "winningPlan" : {
                        "stage" : "FETCH",
                        "inputStage" : {
                                "stage" : "IXSCAN",
                                "keyPattern" : {
                                        "for" : 1
                                },
                                "indexName" : "for_1",
                                "isMultiKey" : true,
                                "direction" : "forward",
                                "indexBounds" : {
                                        "for" : [
                                                "[\"ac3\", \"ac3\"]"
                                        ]
                                }
                        }
                },
                "rejectedPlans" : [ ]
        },
        "executionStats" : {
                "executionSuccess" : true,
                "nReturned" : 4,
                "executionTimeMillis" : 0,
                "totalKeysExamined" : 4,
                **"totalDocsExamined" : 4,**
                "executionStages" : {
                        "stage" : "FETCH",
                        "nReturned" : 4,
                        "executionTimeMillisEstimate" : 0,
                        "works" : 5,
                        "advanced" : 4,
                        "needTime" : 0,
                        "needFetch" : 0,
                        "saveState" : 0,
                        "restoreState" : 0,
                        "isEOF" : 1,
                        "invalidates" : 0,
                        "docsExamined" : 4,
                        "alreadyHasObj" : 0,
                        "inputStage" : {
                                "stage" : "IXSCAN",
                                "nReturned" : 4,
                                "executionTimeMillisEstimate" : 0,
                                "works" : 5,
                                "advanced" : 4,
                                "needTime" : 0,
                                "needFetch" : 0,
                                "saveState" : 0,
                                "restoreState" : 0,
                                "isEOF" : 1,
                                "invalidates" : 0,
                                "keyPattern" : {
                                        "for" : 1
                                },
                                _"indexName" : "for_1",_
                                "isMultiKey" : true,
                                "direction" : "forward",
                                "indexBounds" : {
                                        "for" : [
                                                "[\"ac3\", \"ac3\"]"
                                        ]
                                },
                                "keysExamined" : 4,
                                "dupsTested" : 4,
                                "dupsDropped" : 0,
                                "seenInvalidated" : 0,
                                "matchTested" : 0
                        }
                }
        },
        "serverInfo" : {
                "host" : "DELLRAO-PC",
                "port" : 27017,
                "version" : "3.0.7",
                "gitVersion" : "6ce7cbe8c6b899552dadd907604559806aa2e9bd"
        },


#3.4
```
Which of the following are available in WiredTiger but not in MMAPv1? Check all that apply.
```
- [ ] Collection level locking</br>
- [ ] Covered Queries</br>
- [X] **_Data compression_**</br>
- [ ] Indexes</br>
- [X] **_Document level locking_**</br>
 


