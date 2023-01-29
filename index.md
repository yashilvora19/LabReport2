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

This called the ```handleRequest``` method and went to the else block in the method. Here it executed the first if-statement since the URL did contain ```/add-message```, exectued the nested if-block within that, concatenated a new line character (``` \n ```) and the string to ```myString```, and returned the new string. Hence, the value of ```myString``` changed and got updated. Various methods such as ```contains(), equals(), getPath(), getQuery()``` and ```split()``` were called within these if-blocks.

I repeated this process to add two more messages and display them on the web page.

![Adding 2 more strings](/screenshots/StringServer6.png)

However, when I put ```add-message?``` in the URL without the actual string, I got a **404 error** message. This was expected since I had accounted it for in my code.

![404 error](/screenshots/StringServer7.png)

Hnece, by exploring different inputs, I could see how web server's behaviour in response to each of them and understand which methods and parts of my code were called. 

## Part 2: Analyzing a Bug from Lab 3

In this section, I will look more closely at one of the bugs I worked on during my lab session in week 3. The bug I have chosen is the ```averageWithoutLowest``` method in the ```ArrayExamples.java``` file. The function of this method is to take a double array as an input and find the average of all the elements excluding the lowest value element in that array. 

However, when I gave called this method to an array in my Junit testing an error was thrown. This was my Junit test for the **failure-inducing input**:

```
@Test
  public void averageWithoutLowestRepeated() {
    double[] input3 = {4,4,5,6,7,8};
    assertEquals(6.5, ArrayExamples.averageWithoutLowest(input3), 0);
  }
```
When I ran this test, I was getting an error. The expected value was 6.5 (which is addition of 5,6,7, and 8 divided by 4) but I was getting a value of 5.2. However, when I ran a test using a different array, the Junit passed. Here is the Junit code for the input that **doesn't** induce a failure  :

 ```
@Test
  public void averageWithoutLowestTest() {
    double[] input3 = {4,5,6};
    assertEquals(5.5, ArrayExamples.averageWithoutLowest(input3), 0);
  }
 ```

By looking at these two different outputs for the Junit tests, I was able to see the **symptom** of the code.

![Junit test](/screenshots/Error.png)

Upon looking more closely at the data, I understood that the issue was occuring with arrays in which the lowest value element was repeated. To solve this bug, I introduced a ```count``` variable to the code. This variable counted the number of lowest valued elements there were in an array (if there were repititions) and divided the sum of the remaining values by the length of the ```arr.length - count```. 

**The Bug**

Here is the code that was given to us:

```
// Averages the numbers in the array (takes the mean), but leaves out the
// lowest number when calculating. Returns 0 if there are no elements or just
// 1 element in the array
static double averageWithoutLowest(double[] arr) {
  if(arr.length < 2) { return 0.0; }
  double lowest = arr[0];
  for(double num: arr) {
  if(num < lowest) { lowest = num; }
  }
  double sum = 0;
  
  for(double num: arr) {
    if(num != lowest) { sum += num; }
  }
  return sum / (arr.length - 1);
}
```

Here is the code with the changed logic to remove the bug:

```
// Averages the numbers in the array (takes the mean), but leaves out the
// lowest number when calculating. Returns 0 if there are no elements or just
// 1 element in the array
static double averageWithoutLowest(double[] arr) {
  if(arr.length < 2) { return 0.0; }
  double lowest = arr[0];
  int count = 0;
  for(double num: arr) {
    if(num < lowest) { lowest = num; }
  }
  double sum = 0;
  for(double num: arr) {
    if(num != lowest) {
      sum += num;
    }
    else {
      count++;
    }
  }
  return sum / (arr.length - count);
}
```

By doing making these changes, all the Junit tests passed and the bug was removed.

![Passed tests](/screeenshots/TestsPassed.png)

## Part 3: Reflection of Learnings from Labs

This is the final part of my lab report. I learnt a lot in the past 2 weeks and the lab sessions were extremely valuable to me to facilitate my progress in building my knowledge and learning new things. In my week 2 lab session, I learned more about the ```URLHandler``` interface, building and running a web server both locally and remotely, and got a better understanding about how a web server works and how to program it. In my week 3 lab session, I worked on fixing bugs in various files using Junit tests, understood what symptoms and failure inducing outputs are, and worked with arrays, lists, and linked lists.

Both these sessions pushed me to explore new concepts and helped me learn new things I didn't know before!
