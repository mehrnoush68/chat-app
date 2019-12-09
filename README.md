# Chat Interface

The starting steps for a simple interactive chat interface.

## Steps to complete the assignment

### Outline and suggested timeline

1. [Setup the Layout](#1-setup-the-layout) (15-20 mins)
   - Each student will complete
2. [Custom Styling](#2-custom-styling) (45-60 mins)
   - Group members will divide the tasks
3. [Example Data](#3-example-data) (5-10 mins)
   - Review data as a group to ensure it matches custom styling
4. [Functionality](#4-functionality) (60-90 mins)
   - Each student will take turns typing, others will support

⏱ Please keep an eye on the clock and ensure you are leaving yourself enough time to touch on each section.


### To summarize 

*You will...*

- Have each team member go through the "Setup the Layout" steps independently, testing the layout after each block of css
- Work together to decide on a colour scheme and write the values into a `:root` block as custom CSS properties *(you can revisit the styles again later!)*
- Have one person create a repository and give collaborative access to each other member (you may also create an organization). Once you agree on the layout code and custom properties, modify the local repository and then push the changes to a remote Github repo
- Review the list of [Custom Styling](#2-custom-styling) tasks and decide which member will take on each task. After each styling task is complete, review the overall sight and make necessary adjustments to ensure the entire site is cohesive
- Review the [Example Data](#3-example-data) to ensure all properties needed to accommodate your new custom styling/content are included
- Walk through the [Functionality](#4-functionality), taking turns coding and supporting/researching 


### Submission

1. [ ] Ensure all code is captured in the Github repository
2. [ ] Add all members names and student numbers to the README.md file. Indicate beside each user's name, which of the three "[Custom Styling](#2-custom-styling)" blocks they completed
3. [ ] Setup the site to be viewed live (do this asap!) through `Settings > Github Pages` (change the dropdown from `none` to `master`)
4. [ ] Paste the live link to the Github repository's description (where the url goes, of course)
5. [ ] Create a group DM on Slack with all members and the instructor, then paste send the Github page url only


---
## 1. Setup the layout

*⏱ Time to complete: 15-20 mins*

**🎯 Each student should complete this independently, testing along the way. TEST THE SITE LAYOUT IN ALL SCREEN SIZES AFTER EACH LETTER/STEP**
---

### A. Design system properties

Create a block of styling properties. These are example values, change these as a group (add more if required).

```css
:root {
  --col-bg: #ffffff;
  --col-bg-fg: #222222;
  --col-accent1:  palevioletred;
  --col-accent1-fg: #000000;
  --col-accent2:  plum;
  --col-accent2-fg: #000000;
  --col-accent3:  mediumslateblue;
  --col-accent3-fg: #ffffff;
  --col-action: firebrick;
  --col-action-fg: #ffffff;
  --col-error: tomato;
  --col-error-fg: #000000;
  --font-body: serif;
  --font-heading: sans-serif;
  --animations: 0.3s;
}
```

### B. Document defaults

Setup the document defaults. Adjust these as you see fit. Note the heading has properties that will affect other parts of the layout. Complete everything before adjusting these values.

```css
body {
  background-color: var(--col-bg);
  color: var(--col-bg-fg);
  font-family: var(--font-body);
}
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-heading);
  line-height: 1.25;
  margin: 0.25em 0;
}
h1 {
  font-size: 1.25em;
}
```

### C. Top bar for branding (fixed)

Add styling for the top banner. Modify content or style as needed.

```css
.branding {
  background-color: var(--col-accent2);
  color: var(--col-accent2-fg);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 2;
  width: 100%;
  overflow: hidden;
  text-align: center;
}
```

### D. Side panel of contacts/conversations (fixed)

Style the `other` side panel. Also noticed we're preparing for functionality as well when the `open` class gets added:

```css
.others {
  background-color: var(--col-accent1);
  color: var(--col-accent1-fg);
  position: fixed;
  top: 0;
  left: -100%;
  z-index: 3;
  width: 100%;
  height: 100%;
  padding: 0 1em;
  padding-top: 2.1875em;
}
  .others .panel {
    overflow-y: scroll;
    opacity: 0;
    transition: opacity var(--animations);
  }
.others.open {
  left: 0;
}
  .others.open .panel {
    opacity: 1;
  }
```

### E. Toggle conversation window

This is for the button 

```css
.toggle-others {
  background-color: var(--col-accent3);
  color: var(--col-accent3-fg);
  position: fixed;
  top: 0.5em;
  left: 1em;
  line-height: 1.25;
  z-index: 4;
  padding: 0;
  border: none;
  padding: 0 0.5em;
}
```

### F. Setup conversation window

Adjust the conversation so it doesn't get content stuck under the fixed header.

```css
.conversation {
  padding: 0 1em;
  margin-top: 2.1875em;
}
```

### G. Medium screen styling

Review the following styles for the first media query. 

**Note the drastic change to the functionality of the `.others` sidebar when the `open` class is added or removed. _Try it!_**

```css
@media screen and (min-width: 40em) {
  .others {
    display: block;
    left: 0;
    z-index: 1;
    width: 20em;
    opacity: 1;
    transform: translateX(-20em);
    transition: transform var(--animations);
  }
  .others.open {
    transform: translateX(0em);
  }
  .conversation {
    transition: margin-left var(--animations);
  }
  .others.open ~ .conversation {
    margin-left: 20em;
  }
  .toggle-others {
    position: absolute;
    top: 3em;
    left: auto;
    right: -1.5em;
    width: 1.5em;
    height: 5em;
    padding: 0.25em;
    text-align: center;
  }
  .toggle-others span {
    writing-mode: vertical-rl;
  } 
}
```

### G. Larger screen styling

Add one more media query for larger screens

```css
@media screen and (min-width: 60em) {
  .others {
    width: 30em;
    transform: translateX(-30em);
  }
  .others.open ~ .conversation {
    margin-left: 30em;
  }
}
```


---
## 2. Custom Styling

*⏱ Time to complete: 40-60 mins*

**🎯 Each student will complete one of these for their group**
---

### A. Message block
1. Quickly wireframe a single message block layout, adding all the properties of a `messages` Object that you deem useful/required
2. Review as a group, consider revisions or other configurations before finalizing a choice
3. Sketch the styling (borders, shadows, lines, spacing, shading, etc)
4. Create the HTML for one chat message `article`
5. Fully style the `article` with a class of `.message` using CSS.
6. Create a rule for elements with class `.from-me` to overwrite styles given to `.message` to show it's from the logged in user
7. Create a rule for elements with class `.from-them` to do the same, but show it's from the opposite user


### B. User card
1. Quickly wireframe a list item for a single user, including any relevant information (even if you have to make it up, or the data may be inaccessible)
2. Review as a group, consider revisions or other configurations before finalizing a choice
3. Sketch the styling (borders, shadows, lines, spacing, shading, etc)
4. Create the HTML for the new chat `li`
5. Fully style the `li` with a class of `.usercard` using CSS.
6. Create a rule for elements with class `.selected` so that it's clear from the "Other Conversations" slide out panel that the active conversation is that conversation card
7. Create a modified (if necessary) version of the card with a slightly bigger profile for the `header` of the `#conversation` block of the page, identifying the user you are speaking to. This should be stuck to the top of the `#conversation` block using `position: absolute;`


### C. Input form
1. Quickly wireframe the form that takes the input text from the user, include a few buttons if necessary
2. Review as a group, consider revisions or other configurations before finalizing a choice
3. Sketch the styling (borders, shadows, lines, spacing, shading, etc)
4. Create the HTML for the new chat `form`. Give the msg input component an id of `message`. Give the `<form>` itself an id of `newMsg`. The form will be inside of the `#conversation <footer>`
5. Fully style the `form` with a class of `.newmsg` using CSS. The `<footer>` should be stuck to the bottom of the `#conversation` block using `position: absolute;`
6. Consider what happens when a user has a longer message to type; test to ensure styling accounts for that
7. Create appropriate style for mouse or form interactions, as well as consideration for an `.error` state



---
## 3. Example Data

*⏱ Time to complete: 5-10 mins*

**🎯 Review as a group; Modify to match your custom designs**
---

Here's a set of simple data that can be cut/pasted into the javascript document. Also review this data closely to learn more about the application requirements. Your data may deviate from this any way necessary.

```javascript
const user = {
   id: 456,
   name: 'Charles Babbage',
   img: 'img/456.jpg'
}

const messages = [
   {
      id: 1,
      from: {
         id: 123,
         name: 'Ada Lovelace',
         img: 'img/123.jpg'
      },
      time: {
         date: 1,
         month: 8,
         year: 1843,
         hour: 14,
         minute: 59
      },
      text: `You should check out this little script I just wrote. 😂 lol`
   }
]
```

---
## 4. Functionality

*⏱ Time to complete: 60-90 mins*

**🎯 Students will take turns writing into once code base, while the other group members work in support**
---

### A. Toggle the conversation panel

Check out the JS in action by toggling the open/closed panel

```javascript
document.getElementById(`btnOthers`).addEventListener('click', event => {
  document.getElementById(`others`).classList.toggle('open');
});
```


### B. Single message HTML

Create a function that returns the HTML for a single message (created above):

```javascript
function getMessageAsHtml(msg) {
   return `
   <article>
      <!-- Fill all this in -->
   </article>
   `
}
```

Use template literals add the property values from the `msg` Object that's passed in (will come from `messages`). For example: `<p>${msg.text}</p>`.


### C. Render messages function

```javascript
function renderConversation(arr) {
   document.getElementById('messages').innerHTML = arr.map(getMessageAsHtml).join('');
}
```

To test, call the function by passing it the full Array at the bottom of the js document.

```javascript
renderConversation(messages)
```

**Now you should try to:**
1. Before sending the `messages` Array to `renderConversation()` to be rendered, Research the Array function called `sort()` to put the `messages` Array into chronological order backwards (so that the most recent message is at the bottom).
2. Use `slice()` to only show the 20 most recent messages.


### D. Users/conversations

Create an Array of `conversations` that simply holds Objects with user information, as well as any other useful information you may need.

Complete the exact same steps as above to add all `conversations` to the `#others` panel in the `document`

**Now you should try to:**
1. Before sending the `conversations` Array to its rendering function to be rendered, sort the users alphabetiaclly by their name, by researching the String comparison function `localeCompare()` and combining it with `sort()`


### E. Message customizations

Returning to the `renderConversation` function, customize the messages being displayed in the current conversation.

**Now you should try to:**
Use an `if` statement to determine whether the message's `from` Object property matches the `username` Object (which is the active user). Add the appropriate class: `from-me` for the current user; Otherwise, give it the `from-them` class.


### F. Msg input

Collect information about the message and then create a new Object for the Array. Use the following code:

```javascript
function sendMessage(event, msgs) {
   event.preventDefault();

   const id = (msgs.reduce((highest, m) => (m.id > highest) ? m.id : highest, 0)) + 1; // Unique id

   const now = Date.now(); // The current date and time
   const date = now.getDate();
   const month = now.getMonth();
   const year = now.getFullYear();
   const hour = now.getHours();
   const minute = now.getMinutes();

   const text = event.target.elements.message.value.trim(); // The text

   // 1. Create a new `message` Object here with the data above

   // 2. push() the object onto the parameter `msgs` here

   renderConversation(msgs);  // Re-render the messages
};

document.getElementById('newMsg').addEventListener('submit', e => sendMessage(e, messages))

```

**Now you should try to:**
1. Create a new message Object using the data captured in the function
2. Add the new Object to `msgs` (which is actually the full array!) by researching the Array `push()` method and passing the Object as an argument


### G. Conversation header

Paste the HTML for the other user we're chatting with. Give the appropriate fields an id and fill in the information using javascript.


### H. Conversation footer

Paste the HTML for the `<form>`. Give the appropriate fields an id and fill in the information using javascript.













