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

### 11/26/23

##### onSnapshot(data, function(){codes to execute})

When updating the database, it will automatically resend a new data without loading when fetching the database.

### 12/3/23

##### query(db, where(filter arguments))

It is used for filtering out some of the data when fetching the entire database.

A simple example:
```js
const colRef = collection(db, 'books') //entire database of that section

const q = query(colRef, where("author", "==", "Name")) // filter

getDocs(q) // change from colRef to q where you can get filtered database.
    .then(
      (snapshot) => {
        let books = []; // an array storing data from the database

          books.push({ ...snapshot.docs[0].data(), id: snapshot.docs[0].id})
          console.log(snapshot.docs[0].data(), snapshot.docs[0].id)
        })

```
### 12/8/23 Goal: Able to delete a data without ID.

* Needs to understand JSON Object
* For users, you need to know what data there are so I need to display those data on the webpage.

What I did:
```js
getDocs(colRef)
    .then(
      (snapshot) => {
        let books = [];
        snapshot.docs.forEach((doc) => {
          books.push({ ...doc.data(), id: doc.id})
          document.getElementById("data").innerHTML = document.getElementById("data").innerHTML + `<p>The author is ${doc.data().author} and the title is ${doc.data().title}.</p>`; // fetching all the data into HTML webpage
          } )
        })
```
* Next step: the computer able to search for the id and delete a certain document that user put.

<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
