# MongoDB Assignment

> To import json file in mongo db

For Windows, write this command in bin's cmd

``` 
mongoimport --db mydb1 --collection restro --file c:/samplerestro.json
```
For Ubuntu, write this command in root terminal
```
mongoimport -d mydb1 -c restro --file /home/yogesh/Desktop/mongodb/samplerestro.json      
```
Start Server

> mongod

Start Shell

> mongo

Show Databases

> show dbs

admin     0.000GB
config    0.000GB
employee  0.000GB
local     0.000GB
mydb1     0.005GB
test      0.005GB

> use mydb1

switched to db mydb1

> show collections

restro

> db.restro.find().pretty();
```

#SAMPLE DATA restro.json

{
        "_id" : ObjectId("5d9120baa6746bd7a30005ae"),
        "address" : {
                "building" : "1007",
                "coord" : [
                        -73.856077,
                        40.848447
                ],
                "street" : "Morris Park Ave",
                "zipcode" : "10462"
        },
        "borough" : "Bronx",
        "cuisine" : "Bakery",
        "grades" : [
                {
                        "date" : ISODate("2014-03-03T00:00:00Z"),
                        "grade" : "A",
                        "score" : 2
                },
                {
                        "date" : ISODate("2013-09-11T00:00:00Z"),
                        "grade" : "A",
                        "score" : 6
                },
                {
                        "date" : ISODate("2013-01-24T00:00:00Z"),
                        "grade" : "A",
                        "score" : 10
                },
                {
                        "date" : ISODate("2011-11-23T00:00:00Z"),
                        "grade" : "A",
                        "score" : 9
                },
                {
                        "date" : ISODate("2011-03-10T00:00:00Z"),
                        "grade" : "B",
                        "score" : 14
                }
        ],
        "name" : "Morris Park Bake Shop",
        "restaurant_id" : "30075445"
}
{
        "_id" : ObjectId("5d9120baa6746bd7a30005af"),
        "address" : {
                "building" : "1269",
                "coord" : [
                        -73.871194,
                        40.6730975
                ],
                "street" : "Sutter Avenue",
                "zipcode" : "11208"
        },
        "borough" : "Brooklyn",
        "cuisine" : "Chinese",
        "grades" : [
                {
                        "date" : ISODate("2014-09-16T00:00:00Z"),
                        "grade" : "B",
                        "score" : 21
                },
                {
                        "date" : ISODate("2013-08-28T00:00:00Z"),
                        "grade" : "A",
                        "score" : 7
                },
                {
                        "date" : ISODate("2013-04-02T00:00:00Z"),
                        "grade" : "C",
                        "score" : 56
                },
                {
                        "date" : ISODate("2012-08-15T00:00:00Z"),
                        "grade" : "B",
                        "score" : 27
                },
                {
                        "date" : ISODate("2012-03-28T00:00:00Z"),
                        "grade" : "B",
                        "score" : 27
                }
        ],
        "name" : "May May Kitchen",
        "restaurant_id" : "40358429"
}
```
1. Write a MongoDB query to display all the documents in the collection restaurants

> db.restro.find().pretty();

2. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine for
all the documents in the collection restaurant.

> db.restro.find({},{restaurant_id:1,name:1,borough:1,cuisine:1}).pretty();

3. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine,
but exclude the field _id for all the documents in the collection restaurant.

> db.restro.find({},{restaurant_id:1,name:1,borough:1,cuisine:1,_id:0}).pretty();

4. Write a MongoDB query to display the fields restaurant_id, name, borough and zip code,
but exclude the field _id for all the documents in the collection restaurant.

> db.restro.find({},{restaurant_id:1,name:1,borough:1,"address.zipcode":1,_id:0}).pretty();

5. Write a MongoDB query to display all the restaurant which is in the borough Bronx

> db.restro.find({borough:"Bronx"}).pretty();

6. Write a MongoDB query to display the first 5 restaurant which is in the borough Bronx.

> db.restro.find({borough:"Bronx"}).limit(5).pretty();

7.Write a MongoDB query to display the next 5 restaurants after skipping first 5 which are in
the borough Bronx.

> db.restro.find({borough:"Bronx"}).skip(5).limit(5).pretty();

8. Write a MongoDB query to find the restaurants who achieved a score more than 90.

> db.restro.find({"grades.score":{$gt:90}}).pretty();

9. Write a MongoDB query to find the restaurants that achieved a score, more than 80 but
less than 100.

> db.restro.find({"grades.score":{$gt:80,$lt:100}}).pretty();

10. Write a MongoDB query to find the restaurants which locate in latitude value less than -
95.754168.

> db.restro.find({"address.coord.1":{$lt:95.754168}}).pretty();

11. Write a MongoDB query to find the restaurants that do not prepare any cuisine of
'American' and their grade score more than 70 and latitude less than -65.754168.

> db.restro.find({cuisine:{$ne:"American"},"grades.score":{$gt:70},"address.coord.1":{$lt:-65.754168}}).pretty();

12. Write a MongoDB query to find the restaurants which do not prepare any cuisine of
'American' and achieved a score more than 70 and located in the longitude less than -
65.754168.

> db.restro.find({cuisine:{$ne:"American"},"grades.score":{$gt:70},"address.coord.0":{$lt:-65.754168}}).pretty();

13. Write a MongoDB query to find the restaurants which do not prepare any cuisine of
'American ' and achieved a grade point 'A' not belongs to the borough Brooklyn. The
document must be displayed according to the cuisine in descending order.

> db.restro.find({cuisine:{$ne:"American"},"grades.grade":"A",borough:{$ne:"Brooklyn"}}).pretty().sort({cuisine:-1});

14. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which contain 'Wil' as first three letters for its name.

> db.restro.find({name:{$regex:/^Wil.*/}},{restaurant_id:1,name:1,borough:1,cuisine:1}).pretty();

15. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which contain 'ces' as last three letters for its name.

> db.restro.find({name:{$regex:/.*ces$/}},{restaurant_id:1,name:1,borough:1,cuisine:1}).pretty();

16. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which contain 'Reg' as three letters somewhere in its name.

> db.restro.find({name:{$regex:/.*Reg.*/}},{restaurant_id:1,name:1,borough:1,cuisine:1}).pretty();

17. Write a MongoDB query to find the restaurants which belong to the borough Bronx and
prepared either American or Chinese dish.

> db.restro.find({cuisine:{$in:["American","Chinese"]},borough:"Bronx"}).pretty();

18. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which belong to the borough Staten Island or Queens or Bronxor Brooklyn.

> db.restro.find({borough:{$in:["Staten Island","Queens","Bronxor Brooklyn"]}},{restaurant_id:1,name:1,borough:1,cuisine:1}).pretty();

19. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which are not belonging to the borough Staten Island or Queens or Bronxor
Brooklyn.

> db.restro.find({borough:{$not:{$in:["Staten Island","Queens","Bronxor Brooklyn"]}}},{restaurant_id:1,name:1,borough:1,cuisine:1}).pretty();

20. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which achieved a score which is not more than 10.

> db.restro.find({"grades.score":{$lt:10}},{restaurant_id:1,name:1,borough:1,cuisine:1,"grades.score":1}).pretty();

21. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those
restaurants which prepared dish except 'American' and 'Chinees' or restaurant's name begins
with letter 'Wil'.

> db.restro.find({cuisine:{$not:{$in:["American","Chinese"]}},name:{$regex:/^Wil.*/}}).pretty();

22. Write a MongoDB query to find the restaurant Id, name, and grades for those restaurants
which achieved a grade of "A" and scored 11 on an ISODate "2014-08-11T00:00:00Z"
among many of survey dates

> db.restro.find({"grades.grade":"A",grades:{$elemMatch:{date:ISODate("2014-08-11T00:00:00Z"),score:11}}},{restaurant_id:1,name:1,grades:1}).pretty();

23. Write a MongoDB query to find the restaurant Id, name and grades for those restaurants
where the 2nd element of grades array contains a grade of "A" and score 9 on an ISODate
"2014-08-11T00:00:00Z".

> db.restro.find({"grades.1.grade":"A",grades:{$elemMatch:{date:ISODate("2014-08-11T00:00:00Z"),score:9}}},{restaurant_id:1,name:1,grades:1}).pretty();


24. Write a MongoDB query to find the restaurant Id, name, address and geographical
location for those restaurants where 2nd element of coord array contains a value which is
more than 42 and upto 52

> db.restro.find({"address.coord.1":{$gt:42,$lt:52}},{restaurant_id:1,name:1,address:1}).pretty();

25. Write a MongoDB query to arrange the name of the restaurants in ascending order along
with all the columns.

> db.restro.find().pretty().sort({name:1});

26. Write a MongoDB query to arrange the name of the restaurants in descending along with
all the columns.

> db.restro.find().pretty().sort({name:-1});

27. Write a MongoDB query to arranged the name of the cuisine in ascending order and for
that same cuisine borough should be in descending order.

> db.restro.find().pretty().sort({cuisine:1,borough:-1});

28. Write a MongoDB query to know whether all the addresses contains the street or not.

> db.restro.find({"address.street":{$exists:false}}).pretty();

29. Write a MongoDB query which will select all documents in the restaurants collection
where the coord field value is Double.

 > db.restro.find({"address.coord":{$type:"double"}}).pretty();

30. Write a MongoDB query which will select the restaurant Id, name and grades for those
restaurants which returns 0 as a remainder after dividing the score by 7.

> db.restro.find({"grades.score":{$mod:[7,0]}},{restaurant_id:1,name:1,grades:1}).pretty();

31. Write a MongoDB query to find the restaurant name, borough, longitude and attitude and
cuisine for those restaurants which contains 'mon' as three letters somewhere in its name.

> db.restro.find({name:{$regex:/.*mon.*/}},{name:1,borough:1,"address.coord":1}).pretty();

32. Write a MongoDB query to find the restaurant name, borough, longitude and latitude and
cuisine for those restaurants which contain 'Mad' as first three letters of its name.

> db.restro.find({name:{$regex:/^Mad.*/}},{name:1,borough:1,"address.coord":1}).pretty();
