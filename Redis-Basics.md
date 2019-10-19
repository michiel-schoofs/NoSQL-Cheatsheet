# Redis(Key-Value store)
A key value store simply stores data using a hashmap approach key => value. Easy to use and highly efficient for quick read/write operations. Cheatsheet is an overview of commands demonstrated at [Redis]( http://try.redis.io/).

## Table of contents
* [Simple Commands](#simple-operations)
* [Data Structures](#data-structures)
  * [Lists](#lists)
  * [Sets](#sets)
  * [Hashes](#hashes)
 * [Other operations](#other-operations)

## Simple operations
| Command  | Description |
| ------------- | ------------- |
| SET ***Key*** ***value***   | Associates the given key with the value specified **(will override value if key exists)** |
| GET ***key*** | Retrieves value associated with the given key |
| SETNX ***key*** ***value***| Only associates value if key doesn't exist |
| DEL ***key*** | Deletes key and associated value |
| INCR ***key*** | Will increment value of the given key by 1 (doesn't work if NAN) |

## Data structures
### Lists
Lists are zero based index and can't be set using the normal set or retrieved using the normal get. Do note that delete will still work.

| Command  | Description |
| ------------- | ------------- |
| RPUSH / LPUSH ***key-list*** ***value*** | Pushes value left or right of the list, if the list didn't yet exists also makes the list |
| RRange / LRANGE ***key-list*** ***from*** ***to***|  Will give the list right or left from index ***from*** to index ***to*** (providing -1 in ***to*** will give the entire list |
| RPOP / LPOP ***key-list*** | Will retrieve the most right or left value and delete it from the list , returns it to the user |
| LLen ***key-list*** | Gives the length of the list |

### Sets
Sets differ from lists in the fact that they will not store duplicate values. Putting the value `Unicorn kitty` in a list twice will add two `Unicorn kitty`. Doing the same to a set will only result in one `Unicorn kitty`.

| Command  | Description |
| ------------- | ------------- |
| SADD ***key-set*** ***value*** | Adds ***value*** to the set ***key*** if ***key*** doesn't yet exist make a new set |
| SREM ***key-set*** ***value*** | Removes ***value*** from the set ***key*** |
| SMEMBERS ***key-set*** | Gives all values part of the set |
| SISMEMBER ***key-set*** ***value*** | checks if ***value*** is member of specified set => return 1 if true else 0|
| SUNION  ***key-set-1*** ***key-set-2*** | Returns all the values in set1 and set2|

There's also the concept of Sorted sets but this is almost completely analogue to previous examples you can find the commands [here](https://redis.io/commands#set).

### Hashes
Hashes is a way to associated a set of fields to a given key (like an object). For example assume a `unicorn kitty` with three attributes:

- Awesomeness (a number obviously over 9000)
- Favorite color (rainbow duuuh)
- Name (cutie mcpie)

We want to store this in a way so we can retrieve all values associated with our kitty that's what hashes are for. We would translate our `unicorn kitty` in the following way:

```
HSET kitty:1000 awesomeness 9001
HSET kitty:1000 favColor "rainbow"
HSET kitty:1000 name "Cutie MC Pie"
```
We use the kitty to indicate the kind of object we're dealing with the 1000 is the identifier of this particular kitty. So if we had another rainbow kitty we would use the key kitty:1001. We can add multiple values in one go with `HMSET`

```
HMSET kitty:1001 awesomeness 42 favColor "Void black" name "Dark lord :3"
```
We can retrieve attributes of our kitty very easily: `HGET kitty:1000 name"` Will get me the name, `HGETALL kitty:1001` will get me all attributes linked with this kitty.

We can also delete or increment specific attributes 
```
HINCRBY kitty:1000 awesomness 27
HDEL kitty:1000 favColor
```

## Other operations
| Command  | Description |
| ------------- | ------------- |
| EXPIRE ***key*** ***seconds***| Makes the key delete itself after specified amount of seconds |
| TTL ***key*** | How long before the specified key expires |
