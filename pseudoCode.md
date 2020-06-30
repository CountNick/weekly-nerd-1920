# The importance of pseudocode

## Lost in translation

Some time ago I was making a card game with the help of socket io. When I first got the idea of making a card game I remember thinking it would be kind of hard. Nevertheless I just started coding like I always do. After some time I kept running into issues and I was getting stuck after fixing one issue. This made me think I was working on something that couldn't be done. In the process of making this card game I realized I never really think of a possible solution before I start coding. I just start coding and try to wing it through the process. This never really bothered me before but now I started to realize this was taking me a lot of extra time which wasn't even necessary if I started to think of possible solutions before starting to code.

> Strategy without tactics is the noise before defeat

## Psuedocode to the rescue

I realised that I could plan a strategy out by writing things in pseudocode before actually coding. What is pseudocode you ask? Pseudocode basically is an informal way of programming that does not require any strict programming language syntax or underlying technology considerations. This can for example be done by placing code comments with the steps you have to complete in order to solve your issue and can help you figure things out quicker.


## Example 
Here is a pseudocode example for a login functionality:

```js
// IF userlogin = true
    // API call to get user data
    // Assign data to variables
    // Re-route user to dashboard
// ELSEIF userlogin failed more than 3 times
    // Don't allow more attempts
    // Send user notification email
    // Re-route user to home page
// ELSE
    // Log bad login attempt
    // Show error message
    // Clear login form
```

As you can see the psuedocode doesn't need to be super technical, but making it more detailed makes it easier to write the actual code. The main things this pseudocode focuses on are:

* The logical flow of your program
* Details of the complex parts of your program
* Conssistent format

## Benefits of pseudocode

The best thing about pseudocode is that it allows you to focus on the algorithmwithout worrying about the syntax of a programming language

## Will it work for you?

Writing things out in pseudocode was really beneficial for me. It helps me getting my rough idea's and outlines of what the (piece of code) should do out of my head which makes it easier to test thing out. Starting to code without thinking having a goal can be really frustrating cause you sometimes don't know where to continue from anymore. I would advice every programmer to at least try out pseudocode.

## sources

* [Why you should write more pseudo code](https://medium.com/@yonatandoron/why-you-should-write-more-pseudo-code-a3a27bcffbd4)

* [How to write pseudocode](https://www.geeksforgeeks.org/how-to-write-a-pseudo-code/)

* [The advantages of using pseudocode](https://www.techwalla.com/articles/the-advantages-of-using-pseudocode)

* [How to write pseudocode](https://dev.to/flippedcoding/how-to-write-pseudo-code-2jfe)