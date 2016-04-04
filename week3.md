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
#3.4
```
function queryDocument(options) {

    var query = {};

    if ("overview" in options) {
        query['$or'] = [{'overview':{"$regex":options.overview,"$options":"i"}},{'tag_list':{"$regex":options.overview,"$options":"i"}}]
        /*
           TODO: Write an assignment statement to ensure that if "overview" appears in the 
           options object, we will match documents that have the value of options.overview 
           in either the "overview" field or "tag_list" field of companies documents.

           You will need to use the $or operator to do this. As a hint, "$or" should be the
           name of the field you create in the query object.

           As with the example for options.milestones below, please ensure your regular
           expression matches are case insensitive.

           I urge you to test your query in the Mongo shell first and adapt it to fit
           the syntax for constructing query documents in this application.
        */
    }

    if ("milestones" in options) {
        query["milestones.source_description"] =
            {"$regex": options.milestones, "$options": "i"};
    }

    return query;
    
}
```
```
Successfully connected to MongoDB for query: 0
Successfully connected to MongoDB for query: 1
Query 1 was:{"milestones.source_description":{"$regex":"CMO","$options":"i"}}
Matching documents: 3
Query 0 was:{"$or":[{"overview":{"$regex":"wiki","$options":"i"}},{"tag_list":{"$regex":"wiki","$options":"i"}}]}
Matching documents: 206
Companies found: 123people,3721-internet-assistant,abc2,abc4,addsyou,adventuredrop,alenty,aptera,atlassian,badoo,barablu,beep-interactive,biblewiki,biographicon,bittorrent,bleacher-advisor,bloglines,bluewalks,bojam,bonvoyagee,brainkeeper,brightside-software,burden-butcher,buzznumbers,buzzr,central-desktop,cjreport,coactlive,collectivesys,collegewikis,comindwork,conceptshare,creative-citizen,crosstech-partners,cubetree,curse,dipity,earthscape,etouch-systems,eyes-on-campus,fan-history,fantada,folia,foodista,fosiki,free-ads-australia,gemzies,globalmotion,golightly,greenvoice,groundreport,groupswim,gurus-feet,heekya,hivelive,icitydata,igloo-software,iknolio,indiconews,infoactive-media,infovark,ipads,isayblog,itbrix,itema,jive-software,jixperts,jotspot,jungle-jam-tv,kagtum,kaltura,kerfuffle,klezio,kooky-plan,late-update,locify,lotus-development-corporation,luminotes,lunarr,lunch,mahalo,makesense,mechaworks,meemix,merchantcircle,metreos-corporation,millsberry,mindthrow,mindtouch,mixedink,moodle,moovement,mse360,mywikibiz,myxer,napster,near-time,netcipia,notely,nowpublic,numberzoom,offbeat-guides,omkar-software,one-billion-minds,ontology2,openlink-software,opentext,optify,organic,oversee,palbee,papervitamins,parkopedia,pbworks,people-for-earth,peoplebrowsr,peoplepad,perpetuum-lab,pickle,pilot-systems,pipl,pirillo-open-source-cms-project,planzone,pluggedin,povo,productwiki,produki,publictivity,quifo,red-swoosh,rinen,rivalsoft,scribble-wiki,sharethis,sharpforge,shopwiki,siteheart,social-square,socialtext,socialwrks,soovle,sourcelabs,spiceworks,spock,sports-coach-network,stake,statugle,stixy,swirrl,swurl,sysomos,tabblo,table-booking,tacit-software,tellwiki,the-company-database,theofficialboard,thoof,travellerspoint,travelpod,tunewiki,tupalo,uberspat,umapper,upad,upcoming,urban-airship,urbantastic,valkyrie-movie-wikia,webzzle,weedee,wemind,whiskey-media,whoisi,whynotad,wibokr,wikia,wikicity,wikihow,wikimapia,wikimedia-foundation,wikinvest,wikipock,wikitude,wikiworldbook,wikiyou,worlds-top-brands,y2m,youserbase,zebraspot-design,zembly,zoho-sheet,zoho-writer,zootool
Total employees in companies identified: 9496
Total unique companies: 194
Average number of employees per company: 48
```
