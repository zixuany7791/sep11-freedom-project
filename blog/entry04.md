# Entry 4
##### 3/17/24

I am still currently on stage 2 on Engineering Design Process, which is researching about the tool. Throughout this month, my partner have helped me found out a bug that I wasn't able to notice when I am testing. In which I am somewhat glad that I showed him my testing project and ask him to play around with it.

The bug that he found out for me is that I cannot delete anything else other than the first item on the list. I went back rereading my code to see if I could find out why by just reading it. Rather than having user to type in ID, I have user just type in the book name and the author to delete as it is easier for users. To do that, I created a for loop to loop through every element on the list and use if and else statement to compare each element to the user's input. If it doesn't match, return an error with try and catch statement. However as I am playing around with it. I realized that if I put an else statement inside of a for loop, it breaks the for loop and it wouldn't run anymore.

I tried switching for loop to while loop, it didn't work either so I started to think alternative ways of doing this. If after looping through each list element and still cannot find the user input, I need a way that the computer can tell that it didn't match. I looked up for a way of doing this and break statement catched my eyes.

Break statement basically skip whatever is left over of the function when certain condition have reached. In this case, I added break inside of the if statement where it skips the rest when I found the list element matching the user's input.
```js
// delete document
const deleteBook = document.querySelector('.delete')
deleteBook.addEventListener('submit', function(event) {
  event.preventDefault()
  console.log(deleteBook.author.value)
  console.log(deleteBook.title.value)
  try {
    let i = 0;
    while (i <= books.length){
      console.log(books[i].author)
      console.log(books[i].title)
      if (deleteBook.author.value == books[i].author && deleteBook.title.value == books[i].title) {
        deleteDoc(doc(db, 'book', books[i].id))
        deleteBook.reset()
        { break; }
      }
      i++;
    }
  }
  catch(err){
    document.getElementById("error").innerHTML = "invalid input"
  }

})
```

With this session of code, my loop is finally working properly and can delete items that are not just at the first of the list element.


Throughout this debugging progress, it is very tiring but rewarding because I worked hard and did it and I believe that I learned a lot. I have continued practiced many skills such as debugging and learning how to google. Whenever you are stucked, maybe it is easier to just look up your issue and see if there is a possible solution. However debugging is also a process of learning so instead of googling the problem you have, you try to debug it first to see what is it that you are missing, then you can google for that.


[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
