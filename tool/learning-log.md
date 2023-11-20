# Tool Learning Log

Tool: **Firebase**

Project: **Grading app**

---

### 10/29/23 Main Goal: Setup Firebase

I followed the Net Ninja firebase tutorial to [here](https://www.youtube.com/watch?v=2yNyiW_41H8&list=PL4cUxeGkcC9jERUGvbudErNCeSZHWUVlb&index=4) and I set up a database and I fetch the data from it.
* Challenge: Testing firebase
  * I went from using `import()` to using `require()` and still didn't work
  * William helped me by saying that I am suppose to put `"type": "Module"` inside of the `<script>`

### 10/30/23
Since I have no idea what `then()` is when Net Ninja uses this function when fetching the data, I think it is important for me to learn what it does.

I spent quite a lot of time looking through documentation and learned that `then()` is like an if statement for whether api call worked or not. But I do not understand the rest of the documentation when it is talking about promises.

In the video, Net Ninja also used `forEach()` to fetch every data in the database but since I only put one in, I tried to write codes that are able to fetch one data and I did it after knowing how `forEach()` worked. (My mistake was that I didn't know the proper format of forEach and Net Ninja used the parameter to store the data in so I thought that parameter stored snapshot.docs)

Format:  `.forEach( (arr.length) => {})`

What Net Ninja did:
``` js
snapshot.docs.forEach((doc) => {
books.push({ ...doc.data(), id: doc.id})
} )
```

What I did:
```js
console.log(snapshot.docs[0].data(), snapshot.docs[0].id)
```

### 11/13/23 Goal: Learning functions from firestore

##### getDocs(database)

A function from the module firestore, it is used for fetch the data from the database.

##### addDoc(database, {data})

It is used for adding the data to the database.

##### deleteDoc(doc(database, collection, docId))

It is used for deleting a specfic doc from the database. Note that you will need to import doc **and** deleteDoc in order for it to work.
<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
