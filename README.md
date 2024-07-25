# MongoDB-PlayGround-CRUD
CRUD using MongoDB
Mongosh Commands
Shows dbs/databases (List all databases)
Use sigma (switched to database name as sigma)
db.courses.find()  (Gives all inside data of databases)
For ex-{
  _id: ObjectId('66a12adc4330f2f503847e64'),
  name: 'Java',
  Price: '2000',
  instructor: 'Harry'
}
db.courses.insertOne(name:{JavaScript})

db.courses.find()
 _id: ObjectId('66a12adc4330f2f503847e64'),
  name: 'Java',
  Price: '2000',
  instructor: 'Harry'
}
{
  "_id": {
    "$oid": "66a12e3c78764fe8d99fdb2f"
  },
  "name": "JavaScript"
}



Playground where you can experiment with mongodb

use('SigmaDatabase');

// Insert documents with numeric Price field
db.getCollection('courses').insertMany([
    {
        name: "JavaScript2",
        Price: 10000,
        Instructor: "Aryan B"
    },
    {
        name: "Python for Beginners",
        Price: 15000,
        Instructor: "Samantha K"
    },
    {
        name: "Advanced Python",
        Price: 18000,
        Instructor: "John D"
    },
    {
        name: "Web Development with React",
        Price: 20000,
        Instructor: "Alice W"
    },
    {
        name: "Machine Learning Basics",
        Price: 25000,
        Instructor: "Robert H"
    },
    {
        name: "Data Science with R",
        Price: 22000,
        Instructor: "Emma T"
    },
    {
        name: "Introduction to Java",
        Price: 12000,
        Instructor: "Michael B"
    },
    {
        name: "C++ Programming",
        Price: 13000,
        Instructor: "Jessica L"
    },
    {
        name: "Full Stack Development",
        Price: 30000,
        Instructor: "Daniel M"
    },
    {
        name: "Cyber Security Essentials",
        Price: 27000,
        Instructor: "David R"
    },
    {
        name: "Cloud Computing with AWS",
        Price: 32000,
        Instructor: "David Wallace"
    }
]);

// Query for Price > 28000
const results = db.courses.find({ Price: { $gt: 28000 } }).toArray();
printjson(results);

Output- 
[
  {
    _id: ObjectId('66a14f72bf48bc1af5b090c1'),
    name: 'Full Stack Development',
    Price: 30000,
    Instructor: 'Daniel M'
  },
  {
    _id: ObjectId('66a14f72bf48bc1af5b090c3'),
    name: 'Cloud Computing with AWS',
    Price: 32000,
    Instructor: 'David Wallace'
  }
]
what is cursor .toArray(); converts the cursor returned by the find method into an array. printjson(results); prints the results in JSON format. .find() gives cursor what is that

ChatGPT
In MongoDB, a cursor is an object that allows you to iterate over the results of a query. When you execute a query using the find method, it does not immediately return all the documents that match the query. Instead, it returns a cursor, which is a pointer to the result set of the query. You can then use this cursor to retrieve the documents, either one by one or as a batch.
Key Points about Cursors:
Lazy Evaluation: Cursors use lazy evaluation, which means they don't fetch the documents from the database until you start iterating over them. This is efficient for handling large result sets because it allows you to process documents incrementally without loading all of them into memory at once.
Iteration: You can iterate over a cursor using methods like next() or hasNext(). This is useful for processing documents one at a time.
Batch Size: You can control the number of documents fetched in each batch using the batchSize() method. This can help optimize performance by reducing the number of round trips to the database server.
Example of Using a Cursor
javascript
Copy code
// Assuming a collection named 'courses'
const cursor = db.courses.find({ Price: { $gt: 28000 } });

// Iterate over the cursor and print each document
while (cursor.hasNext()) {
    printjson(cursor.next());
}
Conversion to Array
The toArray() method converts the cursor into an array, which can be useful when you want to work with the entire result set at once. This method fetches all the documents from the cursor and stores them in an array.
Example with toArray()
javascript
Copy code
// Assuming a collection named 'courses'
const results = db.courses.find({ Price: { $gt: 28000 } }).toArray();
printjson(results);
Summary
Cursor: An object that points to the result set of a query and allows iteration over the documents.
Lazy Evaluation: Documents are fetched as you iterate over the cursor, not all at once.
Iteration Methods: next(), hasNext(), etc., to process documents one by one.
Batch Size: Controls the number of documents fetched in each batch.
toArray(): Converts the cursor to an array, fetching all documents into memory.
Why Use Cursors?
Efficiency: Handles large datasets efficiently by not loading all documents into memory at once.
Flexibility: Allows processing documents incrementally, which can be useful for tasks like pagination or streaming data.
By understanding how cursors work, you can write more efficient and flexible MongoDB queries and applications.

use('CrudDb');
//db.createCollection('courses');
let b=db.courses.findOne({price: 20000});
console.log(b);
 Result- {
  _id: ObjectId('66a207d7ffd32a13a55e741b'),
  name: 'Tom',
  price: 20000,
  assignments: 15,
  projects: 40
}
 Note-find and finOne are different .findOne will give the first one it will find in the database which satisfies the condition Find will find all that satisfies the condition but you need to use toArray() as you get cursor which can display only one .
Use toArray() if want more than one.

Also use prinjson() to print it.

use('CrudDb');
//db.createCollection('courses');
let b=db.courses.find({price: {$gt:20000}}).toArray();
printjson(b);

Output-
[
  {
    _id: ObjectId('66a207d7ffd32a13a55e741c'),
    name: 'Emily',
    price: 25000,
    assignments: 8,
    projects: 25
  },
  {
    _id: ObjectId('66a207d7ffd32a13a55e741e'),
    name: 'Jessica',
    price: 22000,
    assignments: 18,
    projects: 35
  },
  {
    _id: ObjectId('66a207d7ffd32a13a55e741f'),
    name: 'David',
    price: 27000,
    assignments: 22,
    projects: 55
  },
  {
    _id: ObjectId('66a207d7ffd32a13a55e7420'),
    name: 'Laura',
    price: 30000,
    assignments: 25,
    projects: 60
  },
  {
    _id: ObjectId('66a207d7ffd32a13a55e7421'),
    name: 'James',
    price: 32000,
    assignments: 30,
    projects: 70
  }
]
 

CRUD in mongoDB

To create a database in MongoDB, use the following syntax:


use('DatabaseName');


This command switches to the specified database, creating it if it doesn't exist.  To Read   To read a database in MongoDB, use the following syntax:
db.collectionName.find(query);
This retrieves documents from the specified collection based on the query.


Update 
use('CrudDb');

db.courses.updateOne({price:0},{$set:{price:100}});
db.courses.updateMany({price:{$gt:2000}},{$set:{price:111}});

Here updateOne() will update price of 0 to price 100 in one only 
If want in all use updateMany(). In updateMany() here we have price of database where price is greater than 2000 will be set into 111.

Delete

use('CrudDb');
db.courses.deleteOne({price:111});
db.courses.deleteMany({price:{$gt:99}});


DeleteOne as usual will delete one only at once. deleteMany() here will delete all which are greater than 99.

To see all operator like gt down below link https://www.mongodb.com/docs/manual/reference/operator/query/  
