# Entry 5
##### 5/5/24

I am currently on Stage 5 on the Engineering Design Process, which is to program RiceGrade with what I have learned over the past months. I have pretty much learned all the concepts that I need for building RiceGrade backend so I believe that I can start contribute to this project. However, throughout this process, I have fully experienced the difficulty of coding with the knowledge of only one tool and not the other. Resulting whenever I attempt contribute my knowledge to the project, I would have to communicate with my partner about the other tool.

This experience happens very fast, right after I downloaded firebase through npm and created a project from [firebase](console.firebase.google.com), I have no idea where to put config so I asked my partner for help since he knows both React and Firebase. Afterwards I attempt to create a login for user to login to their dashboard. Me and my partners agreed to use google as our login for better security so I tried to remake login from what I have on my testing project onto RiceGrade however when I click the button to trigger the google login through popup, it appeared and disappeared immediately. Showing a completely different result from what I tested on my testing website. I asked my partner about this since I have no clue what just happened and how did it happen. So my partner propose idea which is to have user login by email and passwords to create their accounts so that afterwards we could assign roles for the users for better management. Since I have not tried to create login differently, I decided to follow this [youtube video](https://youtu.be/PngrpszT3aY?si=1Tt64EespJnEPa31) since it is a combination of Firebase and React and it also teaches me the usage of `useState`.

```js
 const [isSignUpActive, setIsSignUpActive] = useState(true);

 // function to change register to login or other way around
const handleMethodChange = () =>  {
    setIsSignUpActive(!isSignUpActive)
}
// function to sign up user
const handleSignUp = (event) => {
    event.preventDefault();
    createUserWithEmailAndPassword(auth, email, password)
        .then((userCredential) => {
            // Signed up
            const user = userCredential.user;
            writeData(firstName, lastName, email, roles[role], user.uid)
            // ...
        })
        .catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
            // console.log(errorCode, errorMessage)
            alert(errorMessage);
            // ..
        });
}
// function for user to login
const handleSignIn = (event) => {
    event.preventDefault();
    signInWithEmailAndPassword(auth, email, password)
        .then((userCredential) => {
            // Signed up
            const user = userCredential.user;
            console.log(user)
            // ...
        })
        .catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
            //console.log(errorCode, errorMessage)
            alert(errorMessage)
            // ..
        });
}
```

Throughout this process, I have practice collaborating with my partners and coming up with better solution when something doesn't go well. Whenever I had encounter an issue that I do not have an idea on how to fix, I communicate with my partner to discuss about the solutions to this issue such as asking my partners if they know what and why did my google popup disappeared immediately after appearing for a second. I have also practice "Learning On Your Own" skill throughout this process because I have learned to use `useState` to update the page without reloading the page by watching [youtube video](https://youtu.be/PngrpszT3aY?si=1Tt64EespJnEPa31).


[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
