# Mongo-DB CRUD

As any *RDBMS* It's important to know how to read, write, update and delete to your hearts content. We've already given a brief introduction into what Mongo is in [The introduction](Mongodb-introduction.md). So without further ado lets get to it.

## Table of contents

* [**Insert and create** ](#insert-and-create) (Everything ought to start somewhere)
  * [**Notes on documents**](#notes-on-documents)
* [**Find**](#find) (The select and filter statement of Mongo)
  * [Regular operators](#regular-operators)
  * [Logical operators](#logical-operators)
  * [Querying nested documents](#querying-nested-documents)
  * [Examples of operators](#examples-of-operators)
* **Update** (The way to modify documents)
* **Remove** (All good things come to an end)

## Insert and create

To specify the database you're going to use or work on we use the command: use ***database name***

We can easily create a collection using the following commands:

| Command                                                 | Description                                             |
| ------------------------------------------------------- | ------------------------------------------------------- |
| db.***name-of -collection***.insert(***document***)     | Inserts one document in  the specified collection       |
| db.***name-of -collection***.insertOne(***document***)  | Analogue to the first example                           |
| db.***name-of -collection***.insertMany(***document***) | Insert multiple documents into the specified collection |

### Notes on documents

You can also use arrays or even nest documents <u>within</u> documents like so:

```json
{
    "name":"Rainbow mc sparkle",
    "age":25,
    "decoration":{
    	"shape":"Star"
		"color":"Yellow"
	},
	"childrenNames": ["Louise","Adam",...]
}
```

## Find

Find is the way we query a document. It's in effect a more powerful version of the select statement in SQL. The syntax is as follows:

- db.***Collection-name***.find({***selection-statement***},{***extra options***});

leaving every options blank returns the entire collection

- db.unicorns.find() => entire unicorn collection

The simplest type of selection statement you can do is just checking for an attribute or multiple attributes. The syntax is as follows:

- db.**collection-name**.find({**attribute:value**})
- db.unicorns.find({name:"Rainbow mc sparkle"}) => gives our cute rainbow mc sparkle
- db.unicorns.find({name:"Rainbow mc sparkle", age:25}) => gives our cute rainbow mc sparkle only if they're 25 years old

The real power lays however in the concept of **operators**. Operators give us the ability to write complex queries 

### Regular operators

| Operator                                                   | Description                                                  |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| db.collection.find({ "field" : { $gt: value } } );         | will return everything if the field > value                  |
| db.collection.find({ "field" : { $gte: value } } );        | will return everything if the field >= value                 |
| db.collection.find({ "field" : { $lt: value } } );         | will return everything if the field < value                  |
| db.collection.find({ "field" : { $lte: value } } );        | will return everything if the field <= value                 |
| db.collection.find({ "field" : { $ne: value } } );         | will return everything if the field != value                 |
| db.collection.find({ "field" : { $in: [values,...] } } );  | Will return everything that has field with a value in the specified array |
| db.collection.find({ "field" : { $nin: [values,...] } } ); | Will return everything that has field with a value **not** in the specified array |
| db.collection.find ({'"field"': {$all: [values,...]}})     | Will return everything that has field where all elements are in the specified array |
| db.collection.find({"field":{$size:value}})                | Will return a result if the specified field has a size of the specified value. |
| db.collection.find({"field":{$exist:true/false}})          | Only matches document where the specified field has or doesn't have a value |
| db.collection.find({$where:"**statement**"})               | Allows us to write SQL like statements however is slower and should be avoided |

### Logical operators

Logical operators allow us to combine select queries in a complex way. just like operators allow us to do or, and statements inside if clauses in regular programming.

| Operator | Description |
| -------- | ----------- |
|          |             |
|          |             |
|          |             |
|          |             |



### Querying nested documents

look at the following document:

```json
{
	"name":"Mc pie",
    "children":[{"name": "Jane", "age":36},{"name":"Aria", "age":25}],
    "hobbies":{
        "name":"ski"
    }
}
```

We can query the array and the object using the following query **note the use of "field"**

- db.unciorns.find({"children.name":"jane"}); => Will give me the unicorns with children named Jane
- db.unicorns.find({hobbies.name:"ski"}); => Will give me the unicorns with the hobby skying.

### Examples of operators: 

You can always combine operators on a field like so

- db.unicorns.find({age:{$gte:27,$lte:45}}) => Will give me all unicorns with an age between 27 and 45

Where statements allow us to write queries using JavaScript like where syntax:

- db.unicorns.find({$where: "this.age>=27 && this.age<=45"})

We use the size operator to for example find the unicorns with two decorations:

- db.unicorns.find({decorations: {$size:2}})

The exist operator we can use to find all unicorns that have decorations

- db.unicorns.find({decorations:{$exist:true}})

We can include or exclude fields using the **extra options** parameter of our find:

- db.unicorns.find({decorations:{$exist:true}},{decorations:true}) => will give me the _id field and the decoration field
- db.unicorns.find({decorations:{$exist:true}},{decorations:false,name:false}) => will give me every field besides decoration and name

