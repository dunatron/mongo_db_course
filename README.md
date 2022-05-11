# mongo_db_course

Documenting for reference
https://university.mongodb.com/

# Chapter 1: What is MongoDB?

## The MongoDB Database

Is categorized as a no sql document database

- A Database - Structured way to store and access data
- A NoSQL database - Related tables of data
- NoSQL documentDB - Data in MongoDB is stored as Documents
- Stored in collections - Documents are stored in collections of documents

Collection - an organized store of documents in MongoDB usually with common fields between documents. There can be many collections per database and many documents per collection.

A NoSQL database does not rely on tables, rows and columns to organize data

## What is a Document in MongoDB?

`Document` - a way to organize and store data as a set of field-value pairs.

`Field` - a unique identifier for a datapoint.

`Value` - data related to a given identifier.

`Collection` - an organized store of documents in MongoDB, usually with common fields between documents. There can be many collections per database and many documents per collection.

## What is MongoDB Atlas

- Is a fully managed database, with MongoDB at its core.
- Database as a service
- Database in the cloud
- has many different services and tools available in it, all if which use MongoDB for data storage and retrieval

`Replica Set` - a few connected machines that store the same data to ensure that if something happens to one of the machines the data will remain intact. Comes from the word replicate - to copy something.

`Instance` - a single machine locally or in the cloud, running a certain software, in our case it is the MongoDB database.

`Cluster` - group of servers that store your data.

Advantages of using Atlas

Atlas manages the details of creating clusters for you, simplifying the operation overhead of running and maintaining a database deployment

Atlas has many tools and services within it that are built specifically for the MongoDB Database.

Atlas features go beyond the functionality of organizing and storing data, examples are Charts, Realm, Security features and more.

# Chapter 2: Importing, Exporting, and Querying Data

[Json vs Bson](https://www.mongodb.com/json-and-bson)

## How does MongoDB store data?

When we view or update data it is done in JSON
`JSON`: JavaScript Standard Object Notation
`JSON format`

- Start and end with curly braces `{}`
- Separate each `key` and `value` with a colon `:`
- Separate each `key:value` pair with a comma `,`
- `"keys"` must be surrounded by quotation marks `""`
- in MongoDB `"keys"` are called `"fields"`

### Pros of JSON

- Friendly
- Readable
- Familiar

### Cons of JSON

- `Text-based`: Text-based format, and text parsing is very slow
- `Space-consuming`: Readable format is far from space effecient
- `Limited`: on supports a limited number of data types

MongoDB decided to address these drawbacks

### BSON

Bridges the gap between binary representation and JSON format
Optimized for

- Speed
- Space
- Flexibility

Its goals are

- High performance
- General purpose focus

| Format | Encoding     | Data Support                                                                | Readability       |
| ------ | ------------ | --------------------------------------------------------------------------- | ----------------- |
| JSON   | UTF-8 String | String, Boolean, Number, Array                                              | Human and Machine |
| BSON   | Binary       | String, Boolean, Number(Integer, Long, Float, ...), Array, Date, Raw Binary | Machine only      |

MongoDB stores data in BSON, and you can then view it in JSON

BSON is faster to parse and lighter to store than JSON.

JSON supports fewer data types than BSON

## Importing and Exporting Data

Data in your atlas cluster can be exported to your machine or a different system entirely
The two options when exporting are JSON vs BSON for obvious reasons such as

- if just going from system to system use BSON as it is lighter and faster
- If you intend on reading it use JSON as it is human readable

The below commands are used for importing and exporting from different formats

BSON

- `mongorestore`
- `mongodump`

JSON

- `mongoimport`
- `mongoexport`

### Export

URI string: Uniform Resource Identifier
srv establishes a secure connections

- `mongodump --uri "<Atlas Cluster URI>"` exports data in BSON
- `mongoexport --uri "<Atlas Cluster URI>"` exports data in JSON

- `mongoexport --uri "<Atlas Cluster URI>" --collection=<collection name> --out=<filename>.json`

- `mongodump --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies"`

- `mongoexport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --collection=sales --out=sales.json`

- `mongorestore --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --drop dump`

  - drop dump help with dropping the previous entries so you do not get duplicates

- `mongoimport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --drop sales.json`

## Data Explorer

UI To view the data in atlas

## Find Command

Connect to the Atlas cluster:

```shell
mongo "mongodb+srv://<username>:<password>@<cluster>.mongodb.net/admin"
```

admin has more permissions like getting access to the users. if admin is not appended the default value is test

```shell
show dbs

use sample_training

show collections

db.zips.find({"state": "NY"})
```

It iterates through the cursor

```shell
db.zips.find({"state": "NY"}).count()

db.zips.find({"state": "NY", "city": "ALBANY"})

db.zips.find({"state": "NY", "city": "ALBANY"}).pretty()

```

## Inserting New Documents - ObjectId

If you want to read more about the ObjectId data type, and the ObjectId() function, which generates ObjectId values, [check out this excellent documentation page](https://www.mongodb.com/docs/manual/reference/method/ObjectId/#objectid).
