# Entry 3
##### 2/10/24

I am still currently on stage 2 on Engineering Design Process, which is researching about the tool. In the break I have mainly focused on following [Keithe Paterson tutorial](https://www.youtube.com/watch?v=vuLTzi17k14) on setting up google auth using [firebase website](https://console.firebase.google.com) and I have learned to use `signInWithPopUp` and `signOut` to allows user to sign in and sign out.

With that knowledge, I would like to step ahead and plan out something that I know I will have to do this when I am coding my freedom project, which is using login to send users to different website. However, I haven't really learned anything about the concepts of importing and exporting, so I use the [documentation](https://javascript.info/import-export) to guide me through how to use export and import.

Firstly I separated the firebase config to a single file so I export the file and can just import in all of the file that requires firebase so it looks more organized. Then I created another html file and a javascript file to add `signInWithPopUp` and `signOut`. However, when I am trying to make a button to signIn, it saids that `signIn` is not defined. It is confusing for me to understand why that is because it is not a spelling error yet it cannot find `signIn`.

```html
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
</script>
```
By commenting out codes bit by bit, I realized that the reason why this is not working is because although I imported the javascript file to the html file using `<script>`, it doesn't actually import the function which I have to import the function then use it.

Before:
`<button onclick="signIn()">Hi, Please Log in </button>`

After:
`<button onclick="import('./home.js').then((module) => module.signIn())">Hi, Please Log in </button>`

After that, I tried `onAuthStateChanged`, a function that observe users role and execute code when it got changed. I want to try this function because after the user login, the user should get redirected to their dashboard with their data and I believe that `onAuthStateChanged` can help me accomplish this goal.

With simple codes like
```js
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

I am able to redirect them to the page that user should be at. However, after playing around with the website for a while, I somehow stuck into a infinite loop of loading to the same website. To figure out why that is happening, I have rewriten codes from redirecting user to printing the word logged in when the user role changes. From that, I realized that authObserver was trigger twice when the user role status changes despite I only have called this function one time in this file. It gives me confusion so I commented out the place where I called the function and tried again. This time however, logged in still showed  despite I didn't call the function in this file which gives me confusion because the only other place that I have called this function is in another javascript file in which I believe import shouldn't already called the function already. By playing around with import / export and calling the function. I found out that the best way is just calling the function once without exporting the function to another file.

Throughout this tinkering, I have practice many skills such as debugging, and embracing failures. Learning authentication in firebase is very challenging for me since it took me a lot of time and most of the errors that I got when testing them doesn't actually make sense to me especially for `signIn` function. However, spending a decent amount of time searching what exactly went wrong by commenting out code, rewrite execution code to `console.log()`can leads you to a solution because you understand the problem and how it happened.

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
