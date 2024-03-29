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

### 12/11/23 Goal: complete the next step

* Since the deleteDocs require the document's ID to delete a specific document, I will need to somehow find the ID using title and author.
  * Thinking of using for loop to iterate every document in the `books` array and get the id of that document.

What I did:
```js
let length = books.length;
  for(let i = 0; i < books.length; i++){ // iterate through the database to match the user input
    if (deleteBook.author.value == books[i].author && deleteBook.title.value == books[i].title) {
      deleteDoc(doc(db, 'book', books[i].id))
    }
  }
```

* Next Step: Create an error message

### 12/15/23 Goal: complete the next step

* Used try statement to create an error message

What I did:
```js
// delete document
const deleteBook = document.querySelector('.delete')
deleteBook.addEventListener('submit', function(event) {
  event.preventDefault()
  let length = books.length;
  try {
    for(let i = 0; i < books.length; i++){ // iterate through the database to match the user input
      if (deleteBook.author.value == books[i].author && deleteBook.title.value == books[i].title) {
        deleteDoc(doc(db, 'book', books[i].id))
        document.getElementById("error").innerHTML = ""; //clearing the error message if user input works
      } else{
        throw "invalid input"; // gives an error message
      }
    }
  }
  catch(err){
    document.getElementById("error").innerHTML = err // putting the error message to HTML webpage
  }
  deleteBook.reset() // the input will get back to it's default value after the user click submit.
})
```
### 12/20/23

#### updateDoc(db, {update value})

It is used to update a value of a document that already exist in the
* Same for addDoc

### 12/29/23 Goal: Learn Auth

* Need to import the Auth provider in firebase/auth for the one that you set up in console.firebase.google.com
* Trying out with signInWithPopUp
What I did:
```html
<button class="signInButton">Please Sign In</button>
<script type="module">
  import {
    GoogleAuthProvider, getAuth, signInWithPopup
  } from 'https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js'
  const auth = getAuth()
  auth.useDeviceLanguage();
  const provider = new GoogleAuthProvider();

  // sign in with google popup
  const signIn = document.querySelector('.signInButton')
  signIn.addEventListener('click', function(event) { // when the user click the button, the following code executes
    event.preventDefault()
    signInWithPopup(auth, provider)
      .then((result) => {
        // This gives you a Google Access Token. You can use it to access the Google API.
        const credential = GoogleAuthProvider.credentialFromResult(result);
        const token = credential.accessToken;
        // The signed-in user info.
        const user = result.user;
        // IdP data available using getAdditionalUserInfo(result)
        // ...
      }).catch((error) => {
        // Handle Errors here.
        const errorCode = error.code;
        const errorMessage = error.message;
        // The email of the user's account used.
        const email = error.customData.email;
        // The AuthCredential type that was used.
        const credential = GoogleAuthProvider.credentialFromError(error);
        // ...
      });
  })
</script>
```

### 12/31/23 Goal: Trying out multiple pages

* Learning to use import / export so the files are connected.
* I put firebaseConfig in a separate file call firebaseConfig.js and exported the firebaseConfig, then having every webpage to import the firebaseConfig (very waste of time but looks organized)
* Create a separate html page for sign in and then redirect to the webpage where the database were shown after signing in.

What I did:

```html
<script type="module" src="home.js"></script>
<button onclick="signIn()">Hi, Please Log in </button>
<script type="module">
  import { app } from './firebaseConfig.js'

  import {
      GoogleAuthProvider, getAuth, signInWithPopup, signOut, onAuthStateChanged
  } from 'https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js'


  const auth = getAuth()
  auth.useDeviceLanguage();
  const provider = new GoogleAuthProvider();

  // sign in with google popup
  function signIn() {
      signInWithPopup(auth, provider)
      .then((result) => {
          // This gives you a Google Access Token. You can use it to access the Google API.
          const credential = GoogleAuthProvider.credentialFromResult(result);
          const token = credential.accessToken;
          // The signed-in user info.
          const user = result.user;
          // IdP data available using getAdditionalUserInfo(result)
          // ...
      }).catch((error) => {
          // Handle Errors here.
          const errorCode = error.code;
          const errorMessage = error.message;
          // The email of the user's account used.
          const email = error.customData.email;
          // The AuthCredential type that was used.
          const credential = GoogleAuthProvider.credentialFromError(error);
          // ...
      });
  }
   onAuthStateChanged(auth, (user) =>{
        if (user){
          window.location.href = 'index.html'
        }
    })
</script>
```
* Result: Not working because signIn is not defined (no idea why)

### 1/1/24
* By commenting out codes to see what isn't working, I realized that `type="module"` in script is the reason why signIn is not defined.
* To solve that, I export signIn and then import it in html like this: `<button onclick="import('./home.js').then((module) => module.signIn())">Hi, Please Log in </button>`

* I added another onAuthStateChanged on the index.js (where user suppose to be at after signing in) to make sure that if the user are not sign in, they are redirected to the login page. However after I added onAuthStateChanged, the page starts to refreshes constantly like it is in a infinite loop.

What I did:
```js
// index.js
import { authObserver } from './home.js'

authObserver()
```
```js
// home.js
function authObserver() {
    onAuthStateChanged(auth, (user) =>{
        if (user){
          window.location.href = 'index.html'
        } else {
          window.location.href = 'home.html'
        }
    })
}
authObserver()
export { authObserver }
```

### 1/7/24

* Added Sign Out button

What I did:
```js
//signOut

function signOutFunction () {
  const logOut = document.getElementById("signOut")
  logOut.addEventListener("click", function(event) => {
    signOut(auth)
    .then(() => {
      console.log("You have successfully log out.")
    })
    .catch((err) => {
      console.log(err.message)
    })
  })
}
```

### 1/8/24

* I did some random testing and finds out that somehow you only need one authStateChange observer, or if you have two then it will repeat twice. EVEN IF IT IS IN DIFFERENT FILES!!!
* Found out that deleting doc didn't really work as it should be somehow and haven't found out why.

### 1/29/24 Goal: Rework delete document
* After I played around with the delete document, I found out that it wasn't actually looping because the else statement I put inside the loop makes it so that it only runs one time because else statement break the for loop.

* I tried using while loop to see if anything changed and it apparently didn't.

* I decided to use a variable to determine that they found the document to delete so I can return an error outside of the loop rather than using an else statement inside the loop.

* Second error happens, it says that the author value was undefined in which I don't understand why it happens because I still deleted the book that it suppose to delete.

* By console.log pretty much everything, I realized that the loop is still running even after it deleted the document already.

* I have solved the problem by using `{ break; }` in the if statement so it stops the loop from running because it doesn't need to run anymore.

3/3/24 **React**

* The computer needs to have node.js first doing anything with react.

* We use `npx creat-react-app appName` to get react starter files.

* Use `npm start` instead of `http-server` to test website.

* In `appName/src/index.js`, ReactDOM.render() is where all the react will run at.

* jsx files is a way where it allows programms to type javascript and html without switching sides.

Example:
```jsx
// a very simple function that contains html codes.
function App() {
  return (
    <div className="App">
      <h2>Hello World</h2>
      <ul>
        <li>I am bored</li>
        <li>I am tired</li>
        <li>I want to sleep</li>
      </ul>
    </div>
  );
}


// Then you can call the function in html
<App />
```

### 3/10/24

* Inside of the src folder, you can create a folder called components and put small pieces of code in different jsx files. It is pretty much same thing as my App.js where you export the function and you imported in index.js and render it with ReactDOM

components/Hello.jsx
```jsx
function Hello() {
    return (
        <div>
           <h1>Hello World</h1>
        </div>
    )
}

export default Hello;
```

### 3/24/24

* React Router is a framework that allows you to show different pages in react in a very simple way.

* I followed this (youtube video)[https://www.youtube.com/watch?v=Ul3y1LXxzdU)] to learn how to use browser router

* `Link` from `react-router-dom`is another way of making a hyperlink

* `Route` is where you make connection to the website pages

```js
function App() {
  return (
    <div className="App">
     <BrowserRouter>
          <ul>
            <li>
              <Link to="/Book">Books</Link>
            </li>
          </ul>
        <Routes>
            <Route path="/Book" element={<Book/>} />
        </Routes>
      </BrowserRouter>
    </div>
  );
}
```

* Apparently when you are redirecting to a new page, react will create a new file for you and the content will be what you put in the file that you connected with route.


* You can include CDN in public/index.html

<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
