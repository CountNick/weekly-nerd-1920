# Working on css in a team and a growing codebase

## Team CSS

This article is about structuring CSS when working in a team and a growing codebase. I realised this is something I was struggling with during one of the projects I was working on. It also became appereant to me that I'm not the only one who is struggling with structure when working in a team. That's why I thought it would be a good idea to write something about it so maybe you could learn from my mistakes.


## Good communication

During a the final project of my minor me and a classmate worked on a webapplication as a team.
My classmate told me he had never worked together on a codebase before. I did have some experience working together with people on the same Github Repo. What i usually do when working in a team is start out with setting up some sort of guidelines to follow about coding style, making branches, merging branches, wheter to use css or sass. This time around we forgot to do this. At a certain moment we came to the conclusion that we weren't going about things in the most efficient way. We had one big css file you had to scroll through everytime you wanted to change some rules. This made the development process a bit tedious at first. 

## Components

After doing some research we decided we would make web components out of each ui component in our webapp. This meant that each component got it's own html with it's own custom styling. In the css file of said component would only be css needed for the component it belonged to. All of these isolated css files were compiled to one big css file using Gulp.

For example this is wat the music-player component looked like:

<details><summary>Markup</summary>
<p>

```html
<section class ='controls'>

    <div class="player-info">
    <img class="album-art" src="" width="64px" height="64px" alt="">
    <div class="nowPlaying">
        <p></p>
        <strong></strong>
    </div>
    </div>

    <div class="container">

    <div class="buttons">
        <button class="previousButton"><span class="material-icons">skip_previous</span></button>
        <button class="pauseButton"><span class="material-icons">play_arrow</span></button>
        <button class="nextButton"><span class="material-icons">skip_next</span></button>
    </div>
    
    <input class="progress"type="range" value="0" step="1" name="" id="">

    </div>

    <div class="volume-container">
    <span class="material-icons">volume_up</span>
    <input type="range" class="volume" name="volume" value="1" step="0.1" max="1">
    </div>
</section>
```

</p>
</details>

<details><summary>CSS</summary>
<p>

```css
.controls{
    background: var(--secondary-color);
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    position: fixed;
    bottom: 0;
    padding: .5rem;
    color: white;
    align-items: center;
}

.progress{
      width: 100%;
}

.container{
      width: 30%;
      display: flex;
      flex-direction: column;
      align-items: center;
}

.player-info{
    display: flex;
    align-items: center;
    width: 12em;
}

.buttons button{
    padding: 0.5rem;
    border-radius: 50%;
    border-style: none;
}

.buttons button span{
    color: black;
}

.nowPlaying{
    margin-left: .5rem;
    display: flex;
    flex-direction: column;
    height: 4rem;
    justify-content: space-evenly;
}

.nowPlaying p:first-of-type{
    white-space: nowrap;
}
```

</p>
</details>

This isolated component also had it's own js, but the point is to split components up and isolate the styling and markup from the rest of your components. This makes it easier to find thing you have to work on.

## Sticking to your guns

The web components method worked for us. It made it easier to find and make new css files. Everything went fine until our deadline was coming closer. The design of our webapp gained a lot of momentum which resulted in a lot of stress. We had to do a lot of restyling fast, some things were completely erased and a lot of new ideas come in to play. Because of this we forgot about our isolated component styling method which resulted in some messy css in some components in the end. 

## Conclusion

We found a good method for working on css in a growing project with a team. At some point this went sideways because of our deadline coming closer which I think is something you'll deal with in the workfield as well. I learned a lot by working this way and would certainly advice this method to others. The only tip I would like to give people is to stay consistent with your choices. If you go for isolated components keep them isolated even when in stress, this will save you a lot of work in the long run.


# Sources

* https://www.freecodecamp.org/news/css-naming-conventions-that-will-save-you-hours-of-debugging-35cea737d849/
* https://medium.com/@drublic/css-naming-conventions-less-rules-more-fun-12af220e949b
* https://css-tricks.com/bem-101/
* https://alistapart.com/blog/post/writing-css-on-growing-teams/
* https://stackoverflow.com/questions/3618299/big-development-teams-cant-handle-a-single-css-style-sheet