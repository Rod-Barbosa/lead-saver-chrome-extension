# Scrimba Frontend Career Path - (Leads Saver Chrome Extension - Module 03)

This is a solution to the [Scrimba Frontend Career Path - (Module/App name here)](https://scrimba.com/learn/frontend).

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)


## Overview

### The challenge

Users should be able to Code/Understand:

- const
- addEventListener()
- innerHTML
- input.value
- fucntion parameters
- template strings
- localStorage
- The JSON object
- objects in arrays

### Screenshot

![](./initial.png)
![](./saveTab1.png)
![](./saveTab2.png)
![](./delete.png)



### Links

- Solution Github URL: [https://github.com/Rod-Barbosa/lead-saver-chrome-extension](https://github.com/Rod-Barbosa/lead-saver-chrome-extension)
- Live Site URL: [https://rodrigo-lead-saver-chrome-extension.netlify.app/](https://rodrigo-lead-saver-chrome-extension.netlify.app/)
- May hte next one do a better job at translating a browser extension into a website. 
- If you want to install and see how it works, click the github link, download the files, open your google chrome extensions and point the downloads folder. It should do the trick.

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- JavaScript
- Chrome Dev tools


### What I learned
Making a chrome extension is much easier than it looks like.

To see how you can add code snippets, see below:

This is the only "hard coded" part of my html list of leads
```html
        <ul id="ul-el">
        </ul>
```
The list is rendered dynamicly, after being turned into a string. The string conversion happens for performance purposes, given that innerHTML is taxing. Changing the DOM is never free, and keeping performance costs to a minimum is always a good idea
```js
function render(leads) {
    let listItems = ""
    for (let i = 0; i < leads.length; i++) {
        listItems += `
            <li>
                <a target='_blank' href='${leads[i]}'>
                    ${leads[i]}
                </a>
            </li>
        `
    }
    ulEl.innerHTML = listItems
}
```
Grabbing the current tab on chrome is much easier than it looks. Interesting is that how it actually make sence to have a tab be checked at the same time for "active" and currentWindow status. Maybe you have two broswers open... you want to select the tab you are using, not the one on the background.
```js
tabBtn.addEventListener("click", function(){    
    chrome.tabs.query({active: true, currentWindow: true}, function(tabs){
        myLeads.push(tabs[0].url)
        localStorage.setItem("myLeads", JSON.stringify(myLeads) )
        render(myLeads)
    })
})
```
This saves the Leads after the tab is closed. Allowing for a much better extension. You don't have to keep it open in order to maintain the saved Leads.
```js
localStorage.setItem("myLeads", JSON.stringify(myLeads) )
```

### Continued development

The course is getting more and more interesting. I'm very surprised how educational coding a chrome extension (witha real world use) can be.


### Useful resources

- [Select input color change](https://stackoverflow.com/questions/43427993/change-the-color-of-a-input-field-when-selected?rq=1) - Quick and sweet CSS trick
- [.value](https://stackoverflow.com/questions/11563638/how-do-i-get-the-value-of-text-input-field-using-javascript) - This is always gonna be there. Grabbing the actual value the user is inputting on the browser. This will become second nature and it is nice to know how it works
- [Clear textbox JavaScript](https://stackoverflow.com/questions/4135818/how-to-clear-a-textbox-using-javascript) - Very rarely we want the input field to keep what was just saved
- [Open Link on another tab](https://www.freecodecamp.org/news/how-to-use-html-to-open-link-in-new-tab/) - target="_blank"
- [Double click Event](https://techstacker.com/how-to-detect-double-clicks-with-vanilla-javascript/) - To avoid losing all your leads but accident, delete checks for double click before clearing localStorage
- [Select current Tab Chrome](https://stackoverflow.com/questions/6718256/how-do-you-use-chrome-tabs-getcurrent-to-get-the-page-object-in-a-chrome-extensi) - Easier to go on SO than to go to the google official explanation

**Note: Delete this note and replace the list above with resources that helped you during the challenge. These could come in handy for anyone viewing your solution or for yourself when you look back on this project in the future.**

## Author

- Website - [Rodrigo Portfolio](https://www.gelatodigital.com)
- Frontend Mentor - [@Rod-Barbosa](https://www.frontendmentor.io/profile/Rod-Barbosa)
- Github - [@Rod-Barbosa](https://github.com/Rod-Barbosa)

## Acknowledgments

Thanks again the SO for showing hwo to deal with crome tabs without having to read all the documentation
