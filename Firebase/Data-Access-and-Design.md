# Firestore
Is a `NoSQL` database that supports real-time functionalities. It works very similar to that of `Azure CosmosDb` i.e. works with `Collections` and `Documents`

One should be knowledgeable with basic `NoSQL` database design concepts such as `Embedding` and `Referencing` as you will encounter this a lot when querying data. We won't talk about that in detail here, so be sure to read about it before working on a project that runs in `Firebase`

## General Tip
Imagine a `NoSQL` database as a very very HUGE `JSON` file wherein you will work against a tree-like, hierarchical structure represented by `Collections` and `Documents`


## Collections
Are your `tables` in your `SQL` databases. It holds a "collection" of `documents` that represents a data/object/entity. 

## Documents
Are your `rows` in your `SQL` databases. It is the actual data that holds valuable information about something aka `Entities`. A document **can also hold a few collections** from within. We will discuss further below

## Difference of a Document having a Collection instead of bare Array data/object as a property
Query-wise, when you query for a certain document, **all of it's properties gets queried and returned in the memory (yes, including `arrays`, and nested `objects`)**. These additional data might not be relevant all the time and maybe cost heavy from a performance perspective. The way to workaround this is to **create collections** within a document. 

Suppose you have the order document below:
```
{
  "order": {
    "number": 318311,
    "createdAt": 1608624841719,
    "createdBy": "user1",
    "status": "pending",
    "merchant": "merchant 1",
    "items": [
      {
        "name": "Product 1",
        "price": 69,
        "quantity": 420
      },
      {
        "name": "Product 2",
        "price": 55,
        "quantity": 20
      }
    ]
  }
}
```
Suppose that you are required to display the orders in a tabular manner that will have the columns for order number, created at, created by, status, and the merchant. Naturally, you will query for all the orders and present it to the user. Since the `items` property is an `array of objects` and not a `collection`, every time you query your `orders` collection, all of the `items` will also be included in the result. To solve this, you must create a separate `collection` inside the `order` document. Now, if you query for say `orders/318311` only the first-level data will be returned, unless you explicitly tell `Firestore` to return me the `items` collection along with it

## General Tip

You will find your self working with paths; Everything are path-based. Let's say you have an `orders` `collection` that has an `order` `document` with id `60123`. You can query for this specific data by giving `Firestore` it's path e.g. `firestore.doc('orders/60123')` and it will give you the `order` `document` with id `60123`

---

Read more about `Firestore` here:
https://firebase.google.com/docs/firestore

---

# Data Access
If you know the basics of `NoSQL` database design e.g. `Embedding vs Referencing` you will find it easy to write `Firestore` queries using the official `Angular` library `AngularFire`

## Best Practices
* `Firestore` queries should be placed inside `Service` classes and not in the component. We will still maintain the concept of our `Service Layer` for `Firebase` projects while the `Data Layer` will be the `AngularFirestore` class (as a repository)
* Use `Observables` when binding data from `Firestore` to the view. In this way, every time the data changes from `Firestore`, the change will propagate to all clients i.e. `Angular App`.
* Use `Promises` through `toPromise()` calls in `AngularFire SDK` for transactions i.e. `CRUD`. Most of the time we won't need to subscribe to `CRUD` stuff and these are usually `asynchronous`
* There are thing called `references` in the `Firestore` world. Basically, a document will have a `reference` equivalent in the code that allows you to manipulate that document/collection. If you will be modifying a collection or a document more than once in a single call, make sure to assign the `reference` to a variable so that you won't repeatedly query `Firestore` when you need it