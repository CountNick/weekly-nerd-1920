# Making a SPA MPA hybrid with AJAX in Express

## Introduction

Lately I was working on a web application for someone. As it was my first time doing something like this I had already made the decision to make a server side rendered website without asking if this what the client wanted. During the second week of the project it struck me that what we wanted to make couldn't be done over HTTP requests and we were better of making a clientside webapp. But the thing was we already had a bunch of code which was working and didn't want to start over again. So now we had to choose between a Single Page Web Application(SPA) or a mix between Server Side Rendered and Single Page. The only hickup here was I couldn't find any example on how to make a hybrid web application.

## The problem 

In a traditional website you'd send a request for a website to the server this happens when you type in a url and hit enter. If nothing goes wrong all parts neccassary to make said webpage would be downloaded and displayed on your computer.

![traditional](https://mdn.mozillademos.org/files/6475/web-site-architechture@2x.png)

The problem with this traditional webpage request is that when a user was to interact with the webpage I wanted a part of the webpage to update without it loading the entire page again. As every task the user had to complete was done on one page this would result in a bad user experience.

## The solution

I found out that this can be done with AJAX. AJAX stands for Asynchronous Javascript and XML however this name is misleading because AJAX applications may use XML to transport data, but it is also very common to transport data as plain text or JSON text. With AJAX it's possible to:

* Read data from a web server - after a web page has loaded
* Update a web page without reloading the page
* Send data to a web server - in the background

![AJAX](https://mdn.mozillademos.org/files/6477/moderne-web-site-architechture@2x.png)


<!-- # SPA or SSR

I started of by researching the differences between Single Page Applications and Server Side Rendered pages. The main thing we could not reach with SSR is passing states because the page would refresh if you ought to go to a new page. Keeping track on state is easy to do in a SPA because theres no HTTP request send out which means no page reload, everything basically happens on one page. The only big disadvantage to a SPA is that everything is handled on the clientside, this means that if a user doesn't have javascript the app won't work. 

# Server Side Rendered SPA 

Because it was not possible to progressively enhance the SPA i started looking into rendering a SPA on the server side. However i quickly came to the conclusion this wasn't the right answer for my issue either. A Server Side rendered SPA basically means that the initial page is rendered on the server and sent back to the client. So if a user is not able to use javascript he or she will only be able to see the homepage of the application, and won't be able to interact with it. -->

# AJAX search example

I recalled an example that was given to us by [Declan Rek](https://github.com/decrek/progressive-web-apps-1920/blob/master/examples/movies-example/src/js/search.js). He used a input form to send a query to the server in the background. I just didn't really get how it worked and decided to do some further research on it and try to explain how this works in my own words.

We'll start out by making some simple markup. A basic form with a input of type search:

```html
    <form id="quickSearchForm" method="GET" autocomplete="off" action="/searchResults">
      <button type="submit"><span class="material-icons">search</span></button>
      <input type="search" id="search" name="searchValue" placeholder="Search" data-search-input="input">
    </form>
```

To make the AJAX request we need some javascript code on the clientside as well:
```js
//select the searchbar from the DOM
const searchBar = document.getElementById('search')

//add an event listener on input
searchBar.addEventListener('input', (event) => {
    //the value of what the user is typing
    const userInput = event.target.value

    //the url the action of the form is pointing to, in this case: /searchResults
    const url = document.getElementById('quickSearchForm').getAttribute('action')

    //this will fetch the html from our own server, a query is passed to the route with the user input a, a boolean to check wheter the qquery received was asynchronous and in my case the acces token
    fetch(url + '?query=' + userInput + '&async=true') 
        .then(res => res.text())
        .then(html => {
            //replace the html element you want to replace
            document.querySelector('.search-results').innerHTML = html

        })  
})

```

What happens in this piece of code is that when the user starts typing in the searchbar. The action attribute the form(the method of this formis set to GET) is pointing to(which in my case is the /searchResults route on my express server) is put in a variable called url. We then invoke the fetch() method and pass this the url we we want to fetch from our server and pass the user input as a query and the token as I need that for the external api i am getting data from.
When you start typing in the search input it should how up on your server, you can test this by logging on the server side:

```js
const express = require('express');
const app = express();
const fetch = require('node-fetch');
const port = process.env.PORT || 4000

app
  .use(express.static(path.join(__dirname, 'static')))
  .set('views', __dirname + '/view/pages')
  .set('view engine', 'ejs')
  .get('/searchResults', searchResultsRoute);

app.listen(port, () => {
  console.log(`Dev app listening on port: ${port}`);
});


//this function getss invoked when users get to the /searchResults route
function searchResultsRoute(req, res) {

  let userInput = req.query.searchValue;


  // if the query contains async fetch the data and render the partial
  if(req.query.async){
      fetch(`url-from-api-you-want-toget-data-from/search/q=${userInput}`)
        .then((res) => res.json())
        .then((data) => {
            //only render a partial which has to be updated and give pass the data just fetched with it
            res.render(__dirname + '/view/components/result-list.ejs', {
                trackData: data
            })
        })

  } else {
  // if it's not a ajax request render the whole page
  fetch(
    `url-from-api-you-want-toget-data-from/search/q=${userInput}`)
    .then((res) => res.json())
    .then((data) => {
        //if it doesn't contain the async boolean fetch the data and render the whole page
        res.render('logged-in', {
            trackData: data,
            data: JSON.parse(req.query.data),
            userInput: userInput
        })
    }
}
```

So if the request is Ajax the only thing that needs to be updated is the result-list template which looks like this:

```ejs

<% if (!trackData) { %>
    <p>no results</p>
<% } else {%>
// makes listitem for every track in the trackData array
<% trackData.forEach(track => { %>

    <li class="draggableTrack" draggable="true" > 
        <span class="material-icons">drag_indicator</span>
        <input class="playButton" id="<%= track.uri %>" type="image" src="<%= track.album.images[2].url %>" alt="album-art" width="64px" height="64px">
        <div> <p><%= track.name %></p>
        <p><%= track.artists[0].name %></p>
        </div>
        <a id="<%= track.id%>" class="track-info-link" href=<%= `/track/:${track.id}/` %>>
        <span class="material-icons info">info</span>
        </a>
    </li> 
    
<% }) %>


<% } %>
```


You can make a hybrid app by using this technique in other componenets of your web app that need to be updated. The great thing about making your application this way is that you can do a page refresh when the user is not able to run javascript on the client and render the whole page with the updated results. 

## Sources

<!-- * https://blogs.perficient.com/2015/01/26/mixing-mpa-and-spa-worst-of-both-worlds/
* https://medium.com/@NeotericEU/single-page-application-vs-multiple-page-application-2591588efe58 -->
* https://www.cleveroad.com/blog/single-page-app-vs-multi-page-application-what-to-choose
* https://stackoverflow.com/questions/44080626/how-to-work-with-hybrid-webapp-mpa-and-spa-combined
* https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data
* https://www.w3schools.com/whatis/whatis_ajax.asp
* https://github.com/decrek/progressive-web-apps-1920/blob/master/examples/movies-example/src/js/search.js