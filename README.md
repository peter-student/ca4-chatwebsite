# Submission Report

* Course ID: CS1031
* Student ID: 52212820
* Name: Peter Leeson

## Styling and Design

Consistency of design was one of the main aims when creating the
website, in order for the pages to look both professional and
aesthetically pleasing. This is reflected in the padding, shape of
elements, and colour scheme.

### Global Styling

There are clear gaps between both text and images to aid the
user in knowing where each element starts and ends. These remain
consistent between similar elements, and variations in margin sizes
often serve specific purposes (e.g. user 'join' and 'leave'
notifications have slightly larger margins than message bubbles to
separate them from the main conversation). Most elements also use a
rounded border design of a 7px radius to provide a modern, uniform
appearance. This applies to both clickable and non-clickable content,
including pictures. The presence of emoji symbols throughout the site
makes it more engaging for the user and helps quickly distinguish the
purpose of different items.

### Home Page Styling

Containing the information of the Home page portfolio inside collapsible
buttons was firstly made to make a distinction between the different
content, and secondly to streamline the design of the site. A challenge
of using this design was that the cursor did not automatically change
state into a visible 'pointer' when hovering over the button. This was
solved by using CSS, making it consistent with other buttons and
improving accessibility.

### Chat Page Styling

The 'active users' on the side panel of the chat page are given
individual borders to make them more visible. Similarly, the messages of
the chat are given borders and background colours to imitate the style
of 'chat bubbles' found in other messaging apps. Outgoing messages are
positioned on the right hand of the page and have a lighter colour
scheme, while incoming messages are darker in colour and are positioned
on the left of the page, providing a clear distinction of who each
message is from. Unlike the solid border of chat messages, 'join' and
'leave' notifications have a dashed border and are positioned in the
centre of the screen to distinguish them as separate from the main
conversation. 'Join' messages are green, while 'leave' messages are red
to make their action clearer at a glance. 'Typing' alerts are positioned
on the left and have a grey dotted border, with grey text to represent
their temporary nature. The underlining of the time information and use
of bold text for the usernames helps quickly distinguish the different
elements of the message, bringing focus to the username. The message
form and button have been moved to the bottom of the page to separate it
from the main chat messages.

## Chat Application Functionality

The website runs under the JavaScript runtime server environment
'Node.js'. This allows for the use of both static webpages and further
JavaScript functionality. The use of Express.js allows for the Node.js
functionality to be expanded, making it easier to manage. Meanwhile,
socket.io allows for the real-time sharing of information between the
website and the server, making the chat page functional.

### Custom Usernames

To generate the custom usernames, three separate arrays of adjectives
*'randomAdjective',* nouns *'randomNoun'*, and emojis *'animalEmojis'*
are created (sources for array content at bottom of README.md). A
function is then able to randomly select one of the items in each array
*'getRandomAdjective'* *'getRandomNoun'* *'getRandomAnimalEmoji.'* When
a new user connects to the chat page a variable for each value is
defined *'userAdjective'* *'userNoun'* *'userAnimalEmoji'* and each
value gets assigned an item from the array using the functions. These
values then get combined and assigned to a separate *'userName'*
variable which can then be displayed in the HTML.

Using these custom usernames as opposed to the original string of
numbers makes them more memorable. The animal emojis makes the author of
each message easily visible without having to read the entire username.
However, one downside of this method is the random combinations of words
could have unintended (possibly offensive) meanings, though fixing this
problem was beyond the scope of this project.

### Join/Leave Chat Alert Messages

The creation of chat notifications for a user leaving and joining the
page depends on the use of sockets from socket.io. In the index.js file,
a socket is opened *'socket.on'* to listen for a 'new user'/'disconnect'
message which has been previously created in client.js. This includes a
callback function *'function ()'* which takes the username of the
joining/leaving user. This function then broadcasts and emits a user
join/disconnect message *'socket.broadcast.emit'*. The use of
'broadcast' means that the message does not return to the original user,
only to other connected users. In client.js another socket is opened to
listen for this message and the associated username (which it also takes
as a callback function). The JavaScript appends the
'.messages\_\_history' div using the previously created variable
'messageBox' with the 'innerHTML' command. The HTML code appends,
rather than replaces the existing content due to the use of += rather
than the = assignment operator.

### User Typing Alert Message

A variable is defined in client.js using const for the 'user\_\_typing'
div in chat.html. An EventListener is than created for 'messageForm'
(the input field), waiting for a "keypress". When a keypress occurs,
'socket.emit' emits the message 'userTyping' and the associated
username. In index.js a listener is created for 'userTyping' and similar
to the join/leave chat alerts, broadcasts the message and associated
username to the other connected users. A listener in then opened in
client.js which upon receiving the 'userTyping' message and username,
uses 'innerHTML' to present the message in the 'user\_\_typing' div.
This function uses an = rather than += assignment operator to prevent
multiple messages about the same user typing being displayed. To remove
the typing message from the HTML once the user has sent it, the value of
the div is set to null using 'userTyping.innerHTML = ""' within the
socket for 'chat message.'

## Main Challenges

The main challenge faced was the creation of the listening sockets in
the JavaScript files. Understanding which const variable referred to
each section of HTML required some careful analysis. However, once this
was complete, the process became much easier.

## Sources

The random emoji generator was inspired and adapted from the work of
Erik Martin Jordan, found at
<https://erikmartinjordan.com/get-random-emoji-javascript>

The arrays for the adjectives and nouns were taken from
<https://gist.github.com/ijmacdowell/8325491>

The CSS for the 'Skip to Main Content' functionality of the website was
taken from
<https://www.w3schools.com/accessibility/accessibility_skip_links.php>

The CSS used to centre images was taken from
<https://www.w3schools.com/howto/howto_css_image_center.asp>

The CSS for the form input and message button was inspired and adapted
from <https://github.com/socketio/chat-example/blob/master/index.html>

The CSS to auto-hide the placeholder text in the input field was taken from
<https://stackoverflow.com/questions/9707021/how-do-i-auto-hide-placeholder-text-upon-focus-using-css-or-jquery>
