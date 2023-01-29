# Lab Report 2

This lab report contains content learnt in the 15L lab of weeks 2 and 3. There are 3 parts within this report:
- Part 1: Creating a Webserver
- Part 2: Analyzing a Bug from Lab 3
- Part 3: Reflection of Learnings from Labs

## Part 1: Creating a Web Server

I will be creating a web server using the ```URLHandler``` interface. This web server called ```StringServer``` will keep track of a single string that keeps on getting added to by incoming requests. The page "listens" on localhost at the port specified by us and uses that information to add to the string. Here is the code that I used for this program:

![Code for webs server](/screenshots/StringServer code.png)

I ran the compiled the file and ran it at port 4000. A link was produced and I opened it in my browser to see this:

![Web server](/screenshots/StringServer3.png)

A new server was started from my main method by calling ```Server.start()```. I wanted to print out "hi" on the website, and so added ```add-message?s=hi``` to the URL and got the following result:

![Adding a string](/screenshots/StringServer4.png)

This called the ```handleRequest``` method and went to the else block in the method. Here it executed the first if-statement since the URL did contain ```/add-message```, exectued the nested if-block within that, concatenated a new line character (``` `n ```) and the string to ```myString```, and returned the new string. Hence, the value of ```myString``` changed and got updated. Various methods such as ```contains(), equals(), getPath(), getQuery()``` and ```split()``` were called within these if-blocks.

I repeated this process to add two more messages and display them on the web page.

![Adding 2 more strings](/screenshots/StringServer6.png)

However, when I put ```add-message?``` in the URL without the actual string, I got a **404 error** message. This was expected since I had accounted it for in my code.

![404 error](/screenshots/StringServer7.png)

Hnece, by exploring different inputs, I could see how web server's behaviour in response to each of them and understand which methods and parts of my code were called. 

## Part 2: Analyzing a Bug from Lab 3

In this section, I will look more closely at one of the bugs I worked on during my lab session in week 3. 

## Part 3: Reflection of Learnings from Labs

This is the final part of my lab report. I learnt a lot in the past 2 weeks and the lab sessions were extremely valuable to me to facilitate my progress in building my knowledge and learning new things. In my week 2 lab session, I learned more about the ```URLHandler``` interface, building and running a web server both locally and remotely, and got a better understanding about how a web server works and how to program it. In my week 3 lab session, I worked on fixing bugs in various files using Junit tests, understood what symptoms and failure inducing outputs are, and worked with arrays, lists, and linked lists.

Both these sessions pushed me to explore new concepts and helped me learn new things I didn't know before!
