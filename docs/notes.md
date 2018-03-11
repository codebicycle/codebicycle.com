
# Notes

Read logs

```sh
tail -f log/development.log

less log/development.log
# Shift+F will take you to the end of the file, and continuously display new
# contents. In other words, it behaves just like tail -f.

less +F log/development.log

# to display colors
less -R file.log
```
***

Install gems without sudo

```sh
rbenv local <version>
```
***

Postgres

[What's the default superuser username/password for postgres?][3]

```sh
sudo -u postgres psql postgres

sudo -u postgres createuser -D -A -P myuser
sudo -u postgres createdb -O myuser mydb

psql myuser -h 127.0.0.1 -d db_name

```
[3]:    https://serverfault.com/questions/110154/whats-the-default-superuser-username-password-for-postgres-after-a-new-install

***

Elements outline (dev tools)

```css
* {
    outline: 1px solid green;
}
```
***

HTTP servers (e.g. testing static sites on mobile devices)

```sh
# install (requires nodejs/npm)
npm install http-server -g
#run
http-server -p 8000 --cors
```

```sh
# Python
python -m http.server
# localhost http://127.0.0.1:8000/
```
***

Cinnamon restart `Ctrl+Alt+Esc` (useful when reseting key bindings).

***

Clear terminal `Ctrl+L`

***

Recode, in place, all `.srt` files in current folder, from Central European (1250) to UTF-8 encoding.

```
recode cp1250.. ./*.srt
```
***

Omxplayer specify subtitle

```
omxplayer -o hdmi -r file-name.avi --subtitles file-name.srt
```
***

Download website

```
wget -m -k -nH <http://site.url/>
```
***

Turn off screen using command line

```
xset dpms force off
```
***

Jekyll post's update date

Update post's modification date in the front matter with a git pre-commit hook.

- Create `pre-commit` file in `.git/hooks/` with the following content

        #! /bin/sh
        # Contents of .git/hooks/pre-commit

        git diff --cached --name-status | grep "^M" | while read a b; do
          cat $b | sed "/---.*/,/---.*/s/^update:.*$/update: $(date -u "+%Y-%m-%d")/" > tmp
          mv tmp $b
          git add $b
        done

- Add an `update:` field to post's front matter

        :::yaml
        ---
        title: Post Title
        update:
        ---


- On git commit the `update:` field will update

***

Sublime Text

`Ctrl+R` goto symbol.
With MarkdownEditing package navigate headings.


`F6` toggle spell checking on/off.

***

Run multiple Firefox versions

- download desired firefox version
- extract archive and `cd` into the firefox directory

```bash
cd firefox-52.4.0esr/firefox
HOME=`pwd` ./firefox --no-remote
```

***

Naming

    ::yaml
    is_empty        # boolean
    is_postable()   # return boolean
    post_payment()

Name things based on what they are and not what they look like (css classes).

Javascript example:

```js
fetchFromServer("getSomeTweets", displayTweets);
function displayTweets(err, data) {
  console.log(data.tweets);
}
```
***

Machine Learning

- classifiers
    - support vector machines
- neural networks (nets)
    - deep learning
- reinforcement learning

***

REST
> Client asks for a resource and gets a representation of that resource.

URI
> Every URL is a URI, but not every URI is a URL. ISBN numbers for instance are URI's but not URLS ;)

***

Dynamic Programming, recursion + memoization + guessing

***

Invariants are truths about objects of that class that should endure for the lifetime of the object.

***

The MVC pattern allows the following interactions:

1. A model can change its data depending upon inputs received from the controller.
2. The changed data is reflected on the views, which are subscribed to changes in the model.
3. Controllers can send commands to update the model's state, such as when making changes to a document. Controllers can also send commands to modify the presentation of a view without any change to the model, such as zooming in on a graph or chart.
4. The MVC pattern implicitly includes a change propagation mechanism to notify each component of changes on the other dependent components.
5. A number of web applications in the Python world implement MVC or a variation of it. We will look at a couple of them, namely Django and Flask, in the coming sections.

***

Analysis  
What needs to be done. Output is a set of requirements.  
Visitors of the website need to be able to:

- apply for jobs
- browse, order products

Design  
How things should be done. Output is an implementation specification.
Convert requirements into an implementation specification. (set of classes and interfaces)

- name the objects
- define the behaviors

***

Polymorphism

- multiple forms
- allows objects with different internal structures to have a common interface

***

Algorithms Coursera

Put pseudo-code into programs to understand algorithms better.

Teddy bear programming — explain the problem to somebody, put it in words.

Do one thing  
This implies that the blocks within if statements, else statements, while statements, and so on should be one line long. Probably that line should be a function call.

Book: "Mathematics for Computer Science" by Eric Lehman

***

Probability

    P(A and B) = P(A) * P(B)
    P(A or B) = P(A) + P(B) - P(A and B)

Independent events  
Probability of getting heads on two coin flips

    P(HH) = P(H) * P(H) = 1/2 * 1/2 = 1/4

Gamblers fallacy: after getting n heads in a row the probability of getting another heads is still 1/2 (is not affected by the previous independent draws).

Probability of getting tails on the first flip, heads on the second and tails on the third

    P(THT) = P(T) * P(H) * P(T) = 1/2 * 1/2 * 1/2 = 1/8

***

Circle

Circumference: C = 2πr  
Area: A = πr^2

***

Electricity

Electricity is the movement of electrons.  
Electrons create charge.

Voltage is the difference in charge between two points.  
Current is the rate at which charge is flowing (flow of charge).  
Resistance is a material's tendency to resist the flow of charge (current).


## Javascript and Jquery

The scope of Javascript functions is defined at the time the function is created.  
The scope is determined at the time the function is created, but the values of the variables in the scope are only retrieved at the time the function is called.


`this` is a reference to the object that the function is created inside.

`getElementBy` returns a live nodelist.
`querySelector` returns a static nodelist.


## Docker

A Docker image is the output of a docker build. The build process runs each of the instructions within a Dockerfile.

    docker build

    docker run <image>
      -it interactive terminal
      -d detached
      -p port
    docker stop
    docker start

    docker exec -it   # interact with containers running in the background

- mount x11 socket
- export display
- volume

Jessica Frazelle https://blog.jessfraz.com/


## Google Clean Code Talks by Miško Hevery

Never return a null, instead return a Null Object, e.g. an empty list.

Don't mix instantiation with business logic, use factories, builders.

> Do as little work in constructors as possible.
  Ideally only assignments in constructors.

Law of Demeter  
Asking for something you don't need directly only to get to what you really want.

- Only ask for objects you directly need (operate on).  
- You are not supposed to know about things you don't directly need.  
- Dependency injection, parent object does not make a child, it asks for child. So if child needs a new dependency the parent is not aware.  
e.g. House is not responsible for construction. If it needs a door it asks for one. The HouseFactory is responsible for construction. [video][clean-code-talks]

[clean-code-talks]: https://youtu.be/RlfLCWKxHJ0?list=PL693EFD059797C21E&t=1221

Four biggest untestables

- Location of new operators
- Work in constructors
- Global State (Singletons)
- Law of Demeter violations


## Sandi Metz

> Novice programmers don’t yet have the skills to write simple code.

The message-based perspective yields more flexible applications than does the class-based perspective. Changing the fundamental design question from “I know I need this class, what should it do?” to “I need to send this message, who should respond to it?” is the first step in that direction.

You don’t send messages because you have objects, you have objects because you send messages.

What vs how  
Ask for 'what' you want instead of telling 'how' to do it.

Class is just one way for an object to acquire a public interface; the public interface an object obtains by way of its class may be one of several that it contains.  
It’s not what an object is that matters (class), it’s what it does (interface).

Good design preserves maximum flexibility at minimum cost by putting off decisions at every opportunity, deferring commitments until more specific requirements arrive.

The true purpose of testing, just like the true purpose of design, is to reduce costs.

Incoming messages should be tested for the state they return. Outgoing command messages should be tested to ensure they get sent. Outgoing query messages should not be tested.

Injecting Dependencies as Roles

> Inheritance is for specialization not for sharing code.  
> Inject an object to play the role of the thing that varies.

Null Object pattern
> By returning a null object (i.e. an empty list) there is no need to verify that the return value is in fact a list. The calling function may simply iterate the list as normal, effectively doing nothing. It is, however, still possible to check whether the return value is a null object (e.g. an empty list) and react differently if desired.


Code smells are surface symptoms of deeper problems in the code.

- God object
- feature envy

- long method
- parameter creep
- cyclomatic complexity (too many branches or loops, convoluted logic difficult to follow)
- overly long or short identifiers


Refactoring

- fix complex code first
- fix code smells
- fix low-hanging fruits (code style, conventions)



## Meta

> Find people that make me want to be better or smarter

> People that work hard, high integrity and low ego (how to stat a startup)


- Learn to work with other people in an programming environment (almost everything interesting built today is built in groups).
- Important skill to learn: How to explain something to somebody else.
- Course staff is there to help you learn, use them to learn more quickly and more efficiently.
- Build good habits now (discuss, don't copy).

CS61A Spring 2015, The Structure and Interpretation of Computer Programs, John S. Denero  


> Keep a dozen of your favorite problems present in your mind - Richard Feynman


> Get to the point. What do I get from learning the material? Compact lessons, broken up in bite-sized pieces.


Design is redesign  
> One of the least effective ways to design software architecture is to ignore the software systems that came before us.

> A month of coding can save an hour of architecting



## Resources

Object-Oriented JavaScript by Marcus Phillips - [Udacity][ooj-udacity], [YouTube][ooj-youtube]

Javascript Design Patterns - [Udacity][jdp-udacity]

Parenting101x The Science of Parenting - [Edx][parenting-edx]

JavaScript Domain-Driven Design - Safari



[ooj-udacity]: https://www.udacity.com/course/object-oriented-javascript--ud015
[ooj-youtube]: https://www.youtube.com/playlist?list=PLAwxTw4SYaPmRCRPu9EjK-fWSccPwTOnc

[jdp-udacity]: https://classroom.udacity.com/courses/ud989/lessons/3437288625/concepts/34150192960923

[parenting-edx]: https://courses.edx.org/courses/course-v1:UCSanDiegoX+Parenting101x+2T2017
