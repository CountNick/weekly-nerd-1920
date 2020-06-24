# Instroduction

Lately i was working on an web application for someone. As it was my first time doing something like this i had already made the decision to make a server side website without asking if this what the client wanted. In the second week of the project it kind of struck me that what we wanted to make couldn't be done over HTTP request and we were better of making a clientside webapp. But the thing was we already had a bunch of code which was working and didn't want to start over again.

# SPA or SSR

I started of by researching the differences between Single Page Applications and Server Side Rendered pages. The main thing we could not reach with SSR is passing states because the page would refresh if you ought to go to a new page. Keeping track on state is easy to do in a SPA because you theres no HTTP request send out which means no page reload, evrything basically happen on one page. The only big disadvantage to a SPA is that everything is handled on the clientside, this means that if a user doesn't have javascript the app won't work. 

# Server Side Rendered SPA 

Because it was not possible to progressively enhance the SPA i started looking into rendering a SPA on the server side. However i quickly came to the conclusion this wasn't the right answer for my issue neither. A Server Side rendered SPA basically means that the initial page is rendered on the server and sent back to the client. So if a user is not able to use javascript he or she will only be able to see the homepage of the application, and won't be able to interact with it.

# A hybrid web app

As we had a lot of work done already which we didn't just want to throw away we decided to do some research on hybrid web apps. If we would make a hybrid application we would have the best of both worlds. I started to look for examples but they were pretty much non existant. This is when i remembered a lecture i had from Declan Rek who gave us an example of how to do this using a pice of clientside js.

** Rewrite this piece of code to own **

He showed us the following piece of code to add a livesearch to our searchbar: 
```js
//select the searchbar from the DOM
const searchBar = document.getElementById('search')

//add an event listener on input
searchBar.addEventListener('input', (event) => {
    //the value of what the user is typing
    const userInput = event.target.value

    //the url the action of the form is pointing to, in this case: /searchResults
    const url = document.getElementById('quickSearchForm').getAttribute('action')

    //this will replace the url to what the url would be if a standard search was done except that it happens on the same page
    history.replaceState({}, '','?searchValue=' + userInput + '&token=' + token)

    //this will fetch the html from our own server, a query is passed to the route with the user input a, a boolean to check wheter the qquery received was asynchronous and in my case the acces token
    fetch(url + '?query=' + userInput + '&async=true' + '&token=' + token) 
        .then(res => res.text())
        .then(html => {
            //replace the html element you want to replace
            document.querySelector('.search-results').innerHTML = html

        })
    
})

```

The server side code:
```js
function searchResultsRoute(req, res) {

  let artist = req.query.searchValue;
  let access_token = req.query.token;

  let options = {
    // url: `https://api.spotify.com/v1/search?q=${artist}&type=track%2Cartist&market=US&limit=10&offset=5`,
    method: 'GET',
    headers: { Authorization: 'Bearer ' + access_token },
  };

    // if the query contains async do this
  if(req.query.async){
      fetch(`your-url`,
      options)
        .then((res) => res.json())
        .then((data) => {
            //only render a partial which has to be updated and give pass the data just fetched with it
            res.render(__dirname + '/view/components/result-list.ejs', {
                trackData: data,
                token: access_token
            })
        })

  } else {
      
  fetch(
    `your-url`,
    options
  )
    .then((res) => res.json())
    .then((data) => {
        //if it doesn't contain the async boolean fetch the data and render the whole page
        res.render('logged-in', {
            trackData: data,
            data: JSON.parse(req.query.data),
            token: access_token,
            userInput: artist
        })
    }
}
```