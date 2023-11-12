# Entry 1: Confirm Tool
##### 11/6/23

This year, we are learning Javascript and creating a project using knowledge we will be learning this year. I decided to work with Sam and Benjamin to make a grading app. The purpose of the grading app is to provide a very simple and interactive layout for students and parents to look at their grade and also easier for teachers to import the grades into the website.

To make the grading app, we have decided to use firebase to store multiple data such as login data and student’s grade; and using react to display them in a very simple, comfortable way where users will not be questioning what they are looking at.

Learning both tools is possible, but it will be very challenge due to the amount of time we have so we had to decide who to learn to react and who to learn firebase. Fortunately, Sam knows how react works already so he will be learning firebase so we can have a middle man who can combine them together. Now it is just up to me and Benjamin to decide who is focusing on react or firebase. And we have come to an agreement to tinker with both tools first before making a final decision.

I started learning React using [FreeCodeCamp](https://www.freecodecamp.org/learn/front-end-development-libraries/#react), it introduced me to JSX and it allowed me to write HTML in a javascript file. Sam also taught me and Benjamin about setting up React using the command after installing react `npx create-react-app appName` and have a basic understanding of how starter files work such as you put CDNs in public/index.html.

Sadly, FreeCodeCamp doesn’t have firebase tutorial lessons so I had to find tutorials on youtube to watch and follow. I watch [NetNinja’s](https://www.youtube.com/watch?v=9zdvmgGsww0&list=PL4cUxeGkcC9jERUGvbudErNCeSZHWUVlb) tutorial on firebase because it is short and slow so it is easy for me to understand and catch up. Setting up is very easy, you go to the website and create a database and the website will give you the code to connect your code to the database so you have access to it. The only struggle I have is testing the database. I imported index.js to index.html by using `<script src=”index.js”></script>` but it didn’t work because it said that I cannot use import statement outside of a module. Which confused me because I did exactly what the video showed me and it showed me an error that the video didn’t mention it at all. I googled about this specific error and all I actually have to do is just add `type=”module”` when importing index.js into index.html. Later I learned how to add data to the database on the website and fetch the data simply using a firebase function called `getDocs`. Overall, I find myself having more fun at learning firebase because it is challenging. Meanwhile I believe that I can learn more from firebase than from react and Benjamin said that he wants to focus on react so that is our final decision.

In the Engineering Design Process, we are currently on stage 1 and 2 which is defining and researching the problem. We had defined what we wanted to do and researched and selected the tools that we will be using for the project. Throughout this time, we developed a lot of communication especially on tool selection and discussing the layout of the website and how it is going to work. We met up two times in the library to discuss the project and one time for Sam to teach us how React works.




[Next](entry02.md)

[Home](../README.md)