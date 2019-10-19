# MongoDB
## Table of contents
* [Introduction](#introduction)
## Introduction
Mongodb utilises key-value documents which are very similair to json. 
The real power lays in the fact that documents don't need to provide all values.
unlike regular RDBMS they don't have a fixed diagram that you need to adhere to.

For example: 
```json
{
	"_id": 1,
	"name": "Cutie MC Pie",
	"awesomeness": 9001,
	"favColor": "Rainbow"
}
```

In a relational database we would have the **table** unicorn kitty with a specific row for our adorable Cutie MC Pie. 
The table would contain three attributes: name, favColor and awesomeness. 
What if one of the kitties however had an extra attribute called horn with the value "spikey"?
In a regular rdbms we would have to rethink our design and add a new attribute to our table or work with inheritance.

Document stores are structured in fundamentely the same way we would have a unicorn kitty **collection**. 
Our **document** would be what a row is to our table.
If we wanted to add that extra attribute our document would just contain one fields more:

```json
{
	"_id": 2,
	"name": "Darkness lord :3",
	"awesomeness": 42,
	"favColor": "Void dark",
	"horn": "Spiky"
}
```

**note that all documents need to have a unique _id field**

For this cheatsheet we'll be using mongo db please refer to the manual found [here](https://docs.mongodb.com/v3.2/tutorial/install-mongodb-on-windows/)
for a guide on installing and running it.
