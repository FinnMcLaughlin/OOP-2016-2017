# DT228/DT282 Object Oriented Programming 2016-2017

Resources
---------
* [Webcourses](http://dit.ie/webcourses) - Course code: CMPU2016
* [Slack](https://oop-2016-2017.slack.com)
* [Processing](http://processing.org)
* [The Processing language reference](http://processing.org/reference/)
* [Learning Processing: A Beginner's Guide to Programming Images, Animation, and Interaction (Morgan Kaufmann Series in Computer Graphics)](http://http://www.learningprocessing.com/)
* [The Nature of Code](http://natureofcode.com/)
* [Eclipse](http://eclipse.org)
* [The git manual - read the first three chapters](http://git-scm.com/documentation)
* [A video tutorial all about git/github](https://www.youtube.com/watch?v=p_PGUltnB6w)
* [The Java Tutorial from Oracle](http://docs.oracle.com/javase/tutorial/)
* [Games Fleadh](http://www.gamesfleadh.ie/)
* [The Imagine Cup](https://www.imaginecup.com/)

## Contact the lecturer
* Email: bryan.duggan@dit.ie
* Twitter: [@skooter500](http://twitter.com/skooter500)
* Slack: [oop-2016-2017.slack.com](https://oop-2016-2017.slack.com)

Some assignments from previous years:

[![YouTube](http://img.youtube.com/vi/sPjZSRCmt1U/0.jpg)](https://www.youtube.com/watch?v=sPjZSRCmt1U)

[![YouTube](http://img.youtube.com/vi/0hQt7BKxBcU/0.jpg)](https://www.youtube.com/watch?v=0hQt7BKxBcU)

[![YouTube](http://img.youtube.com/vi/S575a92AsuQ/0.jpg)](https://www.youtube.com/watch?v=S575a92AsuQ)

# Assessments

- [Assignments](assignments.md)

- 8 November 2016 lab test 14%
- 29 November 2016 Assignment 1 submission 20%
- 31 January 2017  Assignment 2 submission - 20%
- Assignment 3 - 30%
- MCQ's - 16%

# Semester 2

# Week 8
- [JDBC Tutorial](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html)
- [The SQLite JDBC Driver](https://bitbucket.org/xerial/sqlite-jdbc/downloads)

# Lab
## Learning Outcomes
- Learn how to set up a JDBC connection to a database
- Learn how to set up the appropriate JDBC driver
- Learn how to run SQL statements and get results through Java
- Learn how to paramaterise an SQL query in Java
- Leran how to encapsulate rows from a table into Java objects

In this lab, we will be building on the JDBC access code we wrote in the class in order to encapsulate the results from an SQL query into an ArrayList of java objects. Firstly clone the repo for the course and import the project AudioViz2 into Eclipse. This will give you the code we made in the class. It probably won't compile without you first setting up the java libraries (which are stored in jar files) that the program depends on. You will need:

- The Processing libraries (core.jar).
- The Minim Libraries (several files).
- The sqlite JDBC driver, which you can [download from here](https://bitbucket.org/xerial/sqlite-jdbc/downloads).

Study the code in the loadTunes method of the TuneFinder class and make sure you understand what each line does. Now make the following changes:

## Part 1

- Make an ArrayList of Tune types as a field in the TuneFinder class called tunes.
- Add an appropriate toString method to the Tune class, that makes a CSV string from the fields of the class.
- Modify the method loadTunes so that it creates a new instance of the Tune class for every row returned and adds it to the arraylist. You should first empty the arraylist by calling clear.
    - I find it useful to make a constructor for the Tune class that takes a ResultSet object as a parameter and constructs the tune from this, rather than include the code for this in the loadTunes method
- Write a method called printTunes that prints all the tunes in the ArrayList, so you can test your loadTunes method.

## Part 2
- Write an overloaded loadTunes method that takes one int parameter for source. It should allow you to pass in the source id as a parameter and it should filter the results to just select tunes with the matching source id. For example, passing 4 will only load tunes that have a source of 4. You should use the PreparedStatement for this, by adding a where clause to the SQL statement. Read [this article](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) that explains how to do it.
- Test this method to make sure it works!
- Write another overloaded method that takes 1 string as a parameter. This should should allow you to do a title search, so it only selects rows where the title contains the string parameter anywhere in the title. For example, passing in "merry" will only load tunes with merry in the title.
- Test this by calling printTunes

## Advanced!
- Write a method called save on the Tune class that saves a tune back to the database. It should use a PreparedStatement with an update sql query. Write some code to test this.
- Include the source name as part of the Tune object. You will also have to join to the source table in your sql statement.

# Week 7
- FFT
- Games Fleadh 

# Week 6
- [Get IntelliJ](https://www.jetbrains.com/student/)
- [Get Eclipse](https://eclipse.org/downloads)
- [Getting started with Eclipse and Processing](https://processing.org/tutorials/eclipse/)
- [An introduction to digital audio from wikipedia](https://en.wikipedia.org/wiki/Digital_audio)

Here is the program we wrote in the class yesterday:

```Java
package ie.dit;

import ddf.minim.AudioInput;
import ddf.minim.Minim;
import processing.core.PApplet;

public class AudioViz extends PApplet {

	Minim minum;
	AudioInput in;

	public void setup()
    {
		minum = new Minim(this);
		in = minum.getLineIn(Minim.MONO, width, 44100, 16);
    }

    public void settings()
    {
        size(530, 329);
    }

    public void draw()
    {
    	background(0);
    	stroke(255);
    	float amp = 100;
        for (int i = 0 ; i < in.bufferSize() ; i ++)
        {
        	line(i, height / 2, i, height / 2 + (in.left.get(i) * amp));
        }
    }

    public static void main(String[] args)
    {
        String[] a = {"MAIN"};
        PApplet.runSketch( a, new AudioViz());
    }
}
```

## Lab

### Learning Outcomes
- Learn how to write Java code using Eclipse
- Lear how to use the Eclipse debugger
- Learn how to link with external jar files in Eclipse
- Learn a little bit about how sound works
- Improve your computational thinking skills by implementing the zero crossings algorithm.

Today lets use Eclipse and Processing with the Minim library to implement a simple pitch detection algorithm called Zero Crossings in order to figure out the musical note that is playing. Feel free to use IntelliJ instead if you prefer.

- Get the code we worked on in the class that implements the music visualiser (above) and get it compiling in your IDE.
- Don't forget to add core.jar and the minim libraries to your Java build path! There is a [tutorial we did yesterday](https://github.com/skooter500/EclipseWithProcessing) that might be useful if you neeed to figure out how to set the Java build path. Make sure and follow the right set of instructions for the version of Processing you have installed.
- Take some time to read through this [introduction to digital audio](http://www.jiscdigitalmedia.ac.uk/guide/an-introduction-to-digital-audio) if you are interested in learning more about how digital audio and sound works. It's very interesting.

Digital audio samples the voltage coming from the microphone and stores these voltages as floating point numbers. For CD quality audio, the microphone is sampled 44100 times per second. If you play a note on an instrument like a tin-whistle or a piano and plot the samples on a graph, it would look something like this:

![Sketch](images/p18.png)

You might notice that this looks a little like a plot of the sin function:

![Sketch](images/p19.png)

However real instruments generate "harmonics" and so it will never be a perfect sine wave. These are caused by the physical properties of the instrument. That's why the plot of the music not is not a perfect sine wave.

Different musical notes are caused by the the air vibrating at different frequencies. For example, when we hear the note D the wave will repeat 293 times in a second. When we hear the note A, the wave will repeat 440 times in a second. A single "wave" in the audio is called a "period".

One simple way of figuring out the frequency, and hence that note that is playing is to count the number of periods that occur in one second. If you notice the waveforms above, you can tell when the period ends, because the signal is above 0 for one sample and then dips to 0 or below in the next sample. By counting the number of times this occurs we can tell how many periods there are. Sometimes we dont have a full second of audio, we only have a short section, but we can still use the zero crossings algorithm and just multiply the result. This segment of audio is called a frame of audio. For example, if we only have 1024 samples and we are sampling at 44100Hz, then we have (1024 / 44100) seconds of audio. This works out at .023 of a second. If we counted 41 crossings in this frame we would multiply by 1 / .023 to get a frequency of 1765. The frequency of the note A6 is 1760, so we could conclude that the note was an A. This technique won't work all the time because of the harmonics, but its a good first step. If you take the time to understand all of the above you will know something cool and amazing.

Using the Minim library, we can set the size of the frame using this code:

```Java
in = minim.getLineIn(Minim.MONO, FRAME_SIZE, sampleRate, 16);
```

You will get the best results by using bigger numbers for this. 1024 will probably work, but 2048 is better.

You can get the frame size using:

```Java
in.bufferSize()
```

You can get the actual sample by using:

```
in.left.get(SAMPLE_INDEX);
```
- Write a method in your program ```public int countZeroCrossings()``` that uses the above two methods to count and return the zero crossings. The algorithm is pretty simple, so I'll let you figure it out for yourself.
- Print out the value using the text command in Processing
- You can use [this resource](http://onlinetonegenerator.com/) to generate sine wave tones of different frequencies to test your program.
- Try singing different notes and see if your program calculates the frequencies correctly. Sing as loud as you like. You are learning. If other people in the lab complain about your singing, tell them I said it was ok to sing loudly in the lab.
- You might need to plug a microphone into your computer if you are using a lab computer. Headphones will work well as a microphone if you have them.

When we take a frequency and get the note name for that frequency, this is called "spelling" the frequency. Here is some Java code for the frequencies of the notes in several octaves of the the D Major scale. For musicians in the class, you will know that D Major has 2 sharps. F# and C#, so the frequencies for the notes F and C are those for F# and C#

```Java
float[] frequencies = {293.66f, 329.63f, 369.99f, 392.00f, 440.00f, 493.88f, 554.37f, 587.33f
			, 659.25f, 739.99f, 783.99f, 880.00f, 987.77f, 1108.73f, 1174.66f};
	String[] spellings = {"D,", "E,", "F,", "G,", "A,", "B,", "C", "D", "E", "F", "G", "A", "B","c", "d", "e", "f", "g", "a", "b", "c'", "d'", "e'", "f'", "g'", "a'", "b'", "c''", "d''"};
```
- Write a method called ```public String spell(float frequency)``` that takes a frequency as a parameter and returns the closest note to the frequency

Here is a video of what your finished program might look like:

[![YouTube](http://img.youtube.com/vi/KOuete3f21c/0.jpg)](http://www.youtube.com/watch?v=KOuete3f21c)

Login to Webcourses and do the MCQ. 

# Week 5
- [Exceptions in Java](http://docs.oracle.com/javase/tutorial/essential/exceptions/)
- [Code for the class](java/SpellChecker)

# Lab
- Learn how to sort an ArrayList using the Collections framework
- Learn how to implement an interface from the JDK
- Get practice constructing an algorithm

In this lab we will implement the ability to give the print the top 10 closest words from the dictionary instead of just printing the closest match. Here is what the output of the final program might look like:


```
$ java ie.dit.Main
Enter a word or quit:
hello
Did you mean:
bell
help
hollow
jelly
well
yellow
all
ball
fall
full
Enter a word or quit:
milk
Correct match
Enter a word or quit:
moon
Correct match
Enter a word or quit:
yellow
Correct match
Enter a word or quit:
bryan
Did you mean:
bread
brown
bad
bag
band
basin
boat
boy
brake
branch
Enter a word or quit:
quit

```

To complete this lab:

- Clone the repo to get the program we worked on in the class and study it carefully.
- [Read this article that explains how you can sort an ArrayList](http://beginnersbook.com/2013/12/java-arraylist-of-object-sort-example-comparable-and-comparator/). If you need to, read it several times!
- You will notice there is an unimplemented method ```public String[] findClosest(String toFind, int howMany)``` in the class Dictionary. At the moment it just returns null, but you should implement this method.
- Modify the Main method to call the new method you wrote that returns a String array instead of the method that returns a String. Make whatever other changes are necessary.
- I strongly suggest you take the time to think about how you would do this. If you can't figure it out, here are [step by step instructions](https://github.com/skooter500/DT228-OOP-2015/blob/master/instructions.md). Only use these if you can't figure it out

# Week 4
- [Unity tutorials](https://unity3d.com/learn/tutorials)
- [Unity project we worked on in the class](https://github.com/skooter500/Demo)

Important Unity stuff to know (there are great tutorials online for all this stuff):
- The Unity editor
- Using Unity with Visual Studio
- GameObjects, GameComponents
- Vector3, Quaternions
- Transforms & parenting
- Exposing c# properties to Unity
- Start & Update methods
- Using tags
- Using the input manager
- Instianting GameObjects from prefabs
- Colliders & triggers
- Rigidbodies, forces & torque

# Lab
## Learning Outcomes
- Learn how the most popular game engine in the world uses OO principles in the design of it's classes

Clone the repo for the project we made in the class on Monday. You can now shoot and hit the falling bricks. Finish off the game by adding a second player controlled tank add scoring & collisions etc. 
- Do the Unity MCQ! 

# Week 3

- [All about the Levenshtein Distance from my PhD thesis. This might be a bit complicated to read](https://github.com/skooter500/DT228-OOP-2015/blob/master/docs/EditDistance.pdf)
- A lecture I gave about the Levenshtein Distance algorithm from a few years ago:

  [![YouTube](http://img.youtube.com/vi/9-8Uj97J85c/0.jpg)](https://www.youtube.com/watch?v=9-8Uj97J85c)

- [Transformation matrices from the Khan Academy (what we did in the tutorial)](https://www.khanacademy.org/math/precalculus/precalc-matrices/matrices-as-transformations/v/transforming-position-vector)
- [Rotation matrices](https://en.wikipedia.org/wiki/Rotation_matrix)

## Lab
### Learning Outcomes
- Have fun implementing the Levenshtein Distance. Its a cool algorithm when you get it to work :-)
- See what matrices are used for
- Build a component of a music information retrieval system

Today lets implement the Levenstein Distance algorithm (also known as the Edit Distance) in Java. Of course you can Google this and you will find lots of solutions online in 5 seconds. But don't do this. Instead, try and implement it from your memory and your notes from the class on Monday. If you weren't here then try asking one of your classmates to explain it to you instead of Googling the solution, or watch the video I put up.

Here is how I suggest you do it:

- Take the Matrix Java project we were working and use it as starter code. You can clone the repo to get it. This also has the transformations we worked on.
- Create a new class called EditDistance.java in the same package as the other classes.
- Create a static method on the class called min3 that takes three float parameters and returns the minimum of these three numbers
- Create a static method on the class called MinimumEditDistance that takes two String parameters, neele and haystack that evaluates the minimum edit distance between needle and haystack. Implement the Levenstein Distance algorithm to calculate this. You should probably print out the matrix by calling the toString method to verify that it is set up correctly
- In the Main class, add this code:

```Java
String sa = "I love DIT";
String sb = "I love Tunepal";
System.out.println("Edit distance between: " + sa + " and: " + sb + " is " + EditDistance.MinimumEditDistance(sa, sb));

sa = "Games Fleadh";
sb = "Imagine Cup";
System.out.println("Edit distance between: " + sa + " and: " + sb + " is " + EditDistance.MinimumEditDistance(sa, sb));
```
- It should print the following:

```
$ java ie.dit.Main
0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0 10.0 11.0 12.0 13.0 14.0
1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0 10.0 11.0 12.0 13.0
2.0 1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0 10.0 11.0 12.0
3.0 2.0 1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0 10.0 11.0
4.0 3.0 2.0 1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0 10.0
5.0 4.0 3.0 2.0 1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0
6.0 5.0 4.0 3.0 2.0 1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0
7.0 6.0 5.0 4.0 3.0 2.0 1.0 0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0
8.0 7.0 6.0 5.0 4.0 3.0 2.0 1.0 1.0 3.0 3.0 5.0 5.0 7.0 7.0
9.0 8.0 7.0 6.0 5.0 4.0 3.0 2.0 2.0 2.0 3.0 6.0 6.0 6.0 7.0
10.0 9.0 8.0 7.0 6.0 5.0 4.0 3.0 2.0 3.0 3.0 7.0 7.0 7.0 7.0

Edit distance between: I love DIT and: I love Tunepal is 7.0
0.0 1.0 2.0 3.0 4.0 5.0 6.0 7.0 8.0 9.0 10.0 11.0
1.0 1.0 3.0 3.0 5.0 5.0 7.0 7.0 9.0 9.0 11.0 11.0
2.0 2.0 2.0 3.0 6.0 6.0 6.0 7.0 10.0 10.0 10.0 11.0
3.0 3.0 2.0 4.0 4.0 5.0 6.0 8.0 8.0 9.0 10.0 12.0
4.0 4.0 3.0 3.0 4.0 6.0 6.0 6.0 7.0 8.0 9.0 10.0
5.0 5.0 4.0 4.0 4.0 7.0 7.0 7.0 7.0 9.0 9.0 11.0
6.0 6.0 5.0 5.0 5.0 5.0 6.0 7.0 7.0 10.0 10.0 10.0
7.0 7.0 6.0 6.0 6.0 6.0 6.0 8.0 8.0 8.0 9.0 10.0
8.0 8.0 7.0 7.0 7.0 7.0 7.0 7.0 8.0 9.0 9.0 11.0
9.0 9.0 8.0 8.0 8.0 8.0 8.0 7.0 9.0 9.0 10.0 10.0
10.0 10.0 9.0 8.0 9.0 9.0 9.0 8.0 8.0 9.0 11.0 11.0
11.0 11.0 10.0 9.0 9.0 10.0 10.0 9.0 9.0 9.0 12.0 12.0
12.0 12.0 11.0 10.0 10.0 10.0 11.0 10.0 10.0 10.0 10.0 11.0

Edit distance between: Games Fleadh and: Imagine Cup is 11.0
```
No MCQ this week

- [Solution to the lab](java/EditDistance)

# Week 2
- [All about Matrices](https://www.khanacademy.org/math/precalculus/precalc-matrices)
- [Matrix multiplication](http://www.mathsisfun.com/algebra/matrix-multiplying.html)
- [Stackoverflow question about static in java](http://stackoverflow.com/questions/413898/what-does-the-static-keyword-do-in-a-class)
- [The matrix class we worked on in the class with a toString method and an add method](java/matrix)
- [Move towards in Processing](processing/MoveTowards)

## Lab

### Learning outcomes
- Get practice writing and calling a static method on a class
- Develop your computational thinking skills by impementing the matrix multiplication algorithm

Today we will be adding methods to the Matrix class to allow matrix multiplication. Check out the [Matrix](java/Matrix) code we worked on in the class that implements methods for matrix addition. This class class, has two methods for addition that allows us to perform the following operations:

- A+= B - This is the *non-static* method add that takes one parameter
- A = B + C - This is the *static* method that takes two parameters.

Read [this article on static in Java](http://stackoverflow.com/questions/413898/what-does-the-static-keyword-do-in-a-class) if you missed the class.

- Write a non-static method mult(Matrix b) that multiplies the current matrix by the b matrix.
- Write a static method mult(Matrix a, Matrix b) that multiplies the a and b matrices together and returns a new matrix.
- Put the following test code into your Main method:

```Java
Matrix a = new Matrix(4, 4);
a.identity();
a.setElement(2, 3, 7);
a.setElement(3, 1, 2);
a.setElement(3, 0, 4);

Matrix b = new Matrix(4, 4);
b.identity();
b.setElement(2, 3, 1);
b.setElement(3, 1, 9);
b.setElement(3, 0, -7);

Matrix2D c;
c = Matrix.mult(a, b); // How to call a static method

System.out.println(a);
System.out.println(b);
System.out.println(c);
```

Your program should output the following:

```
1.0 0.0 0.0 0.0
0.0 1.0 0.0 0.0
0.0 0.0 1.0 7.0
4.0 2.0 0.0 1.0

1.0 0.0 0.0 0.0
0.0 1.0 0.0 0.0
0.0 0.0 1.0 1.0
-7.0 9.0 0.0 1.0

1.0 0.0 0.0 0.0
0.0 1.0 0.0 0.0
-49.0 63.0 1.0 8.0
-3.0 11.0 0.0 1.0
```

Login to webcourses and do this week and last weeks MCQ's 

- [Solution to the lab](java/matrix)

# Week 1
- Compiling and running your first java program (video)

  [![YouTube](http://img.youtube.com/vi/WXftKFCtPrQ/0.jpg)](https://www.youtube.com/watch?v=WXftKFCtPrQ)

## Lab
Today we will make some changes to the Java code we wrote in the class on Monday. Fire up the git bash shell and clone the repo for the course using:

```bash
git clone https://github.com/skooter500/OOP-2016-2017
```
Now cd into the folder java/HelloWorld

To compile the example type:

```bash
javac ie/dit/*.java
```

And to run the program type:

```bash
java ie.dit.Main
```

## Practice making classes in Java

- Create a new subclass of Animal called ```Cat``` with a field for ```numLives```
- Make accessors (set and get methods) for numLives
- Write a Constructor. Call the super class constructor using constructor chaining and also set numLives to be 9
- Write a method called kill. It should subtract 1 from numLives if numLives is > 0 and print the message "Ouch!". If numLives is 0, you should just print the message "Dead"
- In the Main class, construct a Cat instance and in a loop, call kill until the Cat is dead.

## Practice using Polymorphism

- Create another subclass of Animal called Dog
- Make an ArrayList of type Animal 
      - You have to put the code ```import java.util.*;``` at the top of your Java program to use an ArrayList in Java
- Add some instances of the Dog and Cat subclass to the ArrayList and print all the entries in the ArrayList
  - Use a toString() method on the Dog and Cat subclasses to achieve this 

Here is the output of my program:

```
Misty says Woof!
Ouch!
Ouch!
Ouch!
Ouch!
Ouch!
Ouch!
Ouch!
Ouch!
Ouch!
Dead
A dog called Misty
A cat called Top cat has 0 lives
A dog called Tara
```

There is an MCQ so please logon to webcourses and complete it! Some of the questions have multiple answers 

- [Solution to the lab](java/DogsCats)

# Week 13
- [Abstract classes](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)
- [Interfaces](https://docs.oracle.com/javase/tutorial/java/concepts/interface.html)

  Abstract classes & interfaces:

  [![YouTube](http://img.youtube.com/vi/4yVTkG-a6zo/0.jpg)](https://www.youtube.com/watch?v=4yVTkG-a6zo)

# Week 12
- [Dogs Cats & Sheep Polymorphism example](processing/DogsCats)

  Polymorphism:

  [![YouTube](http://img.youtube.com/vi/nt2DzM5n8iw/0.jpg)](https://www.youtube.com/watch?v=nt2DzM5n8iw)

# Week 11
- [YASC Work in Progress (with bullets)](processing/YASC3)

# Week 10
- [Get YASC on Itch](https://skooter500.itch.io/yasc)
- [Get NILL (another game I made in Processing) on Itch](https://skooter500.itch.io/NILL)
- [pushMatrix, popMatrix, translate & rotate example from the class](processing/YASC2)
- [PVectors from the Processing reference](https://www.processing.org/tutorials/pvector/)
- [The particle system from Friday's tutorial class](https://github.com/skooter500/StarParticles) 
- [YASC3 with Physics](processing/YASC3)

Using PVectors:

[![YouTube](http://img.youtube.com/vi/XwniJyTIdec/0.jpg)](https://www.youtube.com/watch?v=XwniJyTIdec)

Daniel Shiffman's introduction to PVectors:

[![YouTube](http://img.youtube.com/vi/7nTLzLf7jUg/0.jpg)](https://www.youtube.com/watch?v=7nTLzLf7jUg)

## Lab
### Learning Outcomes
- Learn how to use PVectors
- Learn how to implement realistic physics by implementing Newton's Laws of Motion

Modify the code we worked on on the class on Monday so that the ship moves with realistic physics. You should use PVectors in your solution. The three equations you need to implement are:

A = F / m

V = V + A * t

P = P + A * t

Where A = Acceleration, V = Velocity, P = Position, t = time 

Force is measured in Newtons and is a vector quantity, so it has magnitude and direction. When you press the w and s keys, instead of moving the position vector, you should create force vector in the direction of the forward vector. To do this, take the forward vector and multiply by the newtons of force you want to apply. I used 100 Newtons of force in my solution.


After you generate the force you need to write code to implement the 3 equations above. 
- Calculate the acceleration due to the force
- Calculate the new velocity
- Update the position based on the velocity and time.

I added the following fields to the Ship class to do this:

- force, power, timeDelta, velocity and acceleration

If you implement this correctly, your ship will accelerate and move realistically. If you want to implement friction, so that the ship slows down, a simple way to do this is to just multiply the velocity by 0.99f each frame. This removes 1% of the velocity. Here is what my sketch looks like:

[![YouTube](http://img.youtube.com/vi/grz4niYV_bs/0.jpg)](https://www.youtube.com/watch?v=grz4niYV_bs)

Some ideas to try:
- Make the keys used to control the ship fields in the Ship class, so you can instantiate several ships controlled with different keys
- Have the Ship draw a trail
- Implement gravity

# Week 9
- [The map method example from Tuesday's class](processing/mapExample)
- [YASC Work in progress](processing/YASC1)
- [YASC on github](http://github.com/skooter500/YASC)

# Lab
- [Lab Test 1](https://github.com/skooter500/OOP-LabTest1-2016)
- [SOlution](https://github.com/skooter500/StarMap)


# Week 8
- [Lab test 2](https://github.com/skooter500/irishEconomy/)
- [Radar example implemented using various techniques](processing/RadarExample)
- [Detecting multiple key presses in Processing](processing/multipleKeys)
- [Timers](processing\timers)
- [Formatting numbers](processing/decimalFormat)

# Week 7
- [Hashmaps in Processing](https://processing.org/reference/HashMap.html)
- [Iterating over a HashMap](http://stackoverflow.com/questions/1066589/iterate-through-a-hashmap)
- All about git

[![YouTube](http://img.youtube.com/vi/p_PGUltnB6w/0.jpg)](https://www.youtube.com/watch?v=p_PGUltnB6w)

# Lab
### Learning Outcomes
- Learn how to use the main features of git via the git bash shell

This lab is all about practicing using git and github. This will work best if you for a group of 2, so that you can get experience collaborating with someone on a project through git. Firstly, make sure you know what the following bash commands do. Fire up the bash shell and try them out. There are lots more, but these are the most common ones I use. Google them and try them out!

```
pwd
ls
ls -a
cd
mkdir
mv
find
grep
```

Note, folders in the bash shell are seperated using / and in Windows explorer you should have the following options checked:

- Show file name extensions
- Hidden files

You will find these options on the View tab of any Windows Explorer window

Also from the bash shell, you can use TAB to complete commands.

Setting up git
- I recommend you install [git for Windows](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) rather than the github client. You can optionally install [SourceTree](https://www.sourcetreeapp.com/) which is a nice git gui program that allows you to *diff* commits (view the changes) amongst lots of other cool stuff.
- The first time you try and do a commit or a push you may have to run come commands to set up your email address and username. Just follow the instructions to do this.
- At some stage you should read the [first 3 chapters of the git manual](https://git-scm.com/documentation). This is pretty much all you need to know.

Note! Select the text using your mouse in the bash shell window and it will get copied to the clipboard. Press Ctrl + Ins to paste.

Basic stuff
- Create a project in Processing and save it somewhere
- Fire up the bash shell and use cd to navigate to the project folder
- Type ```git init``` in the project folder to create an empty git repo. Notice that a new hidden folder called .git will appear in the folder
- Create the project on your github account on github.com. Dont forget to create a .gitignore and a readme.
- Get the url of the new repo and type:
  - ```git remote add origin THE_URL_OF_YOUR_REPO```
- Type ```git pull origin master``` to get the changes from the server. Type ```la -a``` and you should see the new files listed.
- Type ```git add .``` to add your local changes to the staging area
- Type ```git commit -m "some message"``` to make a commit
- Type ```git push --set-upstream origin master``` This creates the connection between your master branch and the master branch on the server
- Type ```git push``` to send your changes to the server

Rolling back to a previous commit
- Make a few more commits and push them
- Type ```git log``` to see the history of your branch and see the 40 digit hexedecimal id's of your commits. It should look something like this

  ```
  commit 7ccd905733dc710ecf38b0431d1143528b5dc1c7
  Author: skooter500 <skooter500@gmail.com>
  Date:   Thu Apr 14 10:03:17 2016 +0100

      Added todays lab

  commit 4b46bea9d2ccd434076310049a5553ccc241adc6
  Author: Bryan Duggan <skooter500@gmail.com>
  Date:   Fri Mar 25 12:55:44 2016 +0000

      classes and bullets example

  commit 6e949c599f038209c9b22da99d5b014a7c47387a
  Author: Bryan Duggan <skooter500@gmail.com>
  Date:   Thu Mar 3 09:15:18 2016 +0000

      broken link

  ```


- Copy one of the 40 digit ids and type ```git checkout THE-40-DIGIT-ID``` Open up your sketch and you should see it has reverted to the old version.
- Type ```git checkout master``` and the head pointer will move to the head of the branch (the latest commit). Open up your sketch and you should see it has changed to the latest version

Rolling back to a previous commit and making a new branch
- If you want to go back to an old version of a project and make changes, you will often see articles on stack overflow etc saying that you should hard reset the head. I recommend that you don't do this as this will delete the subsequent commits on the branch and you might want to get these changes back sometime. Instead, the best thing to do is make the changes on a new branch.
- Checkout one of the old commits again. Make some changes to the sketch
- Type ```git checkout -b my_new_branch``` You can call the branch something different if you want! The -b flag means create the new branch.
- Add and commit your changes to the new branch
- Now switch back to the master branch by typing ```git checkout master```. Open your sketch and verify that you are at the latest version of the project on the master branch.
- You can switch branches at anytime by typing ```git checkout THE_BRANCH_NAME```
- If you want to send this new branch to the server, checkout the branch (no -b flag this time) and type:
  - ```git push --set-upstream origin my_new_branch```
  - ```git push```

Deleting files
- git will normally just store files that have been added or modified in a commit. Files that are deleted don't get deleted in the commit so that if you checkout that commit, the files that you deleted will reappear. If you have deleted files in a commit you should use ```git add . --all```. Try it!

Branching
- You can create multiple branches in git if you want to try new stuff without screwing up your project. In fact it is common to create a new branch every time you want to add a new feature and then merge the branch into the master branch when the feature is completed. Lets try this.
- Type ```git checkout master``` to switch to the head of the master branch
- Type ```git branch``` This shows you what branch you are currently on. You can also type ```git branch --all`` to show all the branches.
- Type ```git checkout -b test_branch``` to create a new branch and switch to it
- Make some changes to to your Processing sketch and save them
- Add and commit these changes.
- To send this new branch to the server type:
  - ```git push --set-upstream origin test_branch```
  - ```git push```
- Type ```git checkout master``` to switch to the master branch and check your Processing sketch to make sure your changes are gone.
- Type ```git checkout test_branch``` and open the Processing sketch to make sure your changes are back again
- Type ```git checkout master``` to switch to the master branch again
- Now lets merge the test_branch changes into the master branch. Type ```git merge test_branch``` to do this
- Open your sketch and see that the changes you made on the test_branch have been merged in.
- Add and commit your merged changes.


Dealing with merge conficts
- Often, git will merge edits in files automatically, but merge conflicts can occur whenever commits have edits on the same line of the same file. This can happen even when only one person is working on a project. When this happens, git will tell you what files are causing problems and mark up the files with the changes from both commits.
- Give your team mate permission to commit to the repository. To do this, go to Settings | Collaborators and add their github id. Your team mate can clone the repository by typing:
  - ```git clone THE_URL_OF_THE_REPO```
- Now both of you should make some edits to the same file. Make some edits on the same lines of the file and on different lines of the file
- Your team mate should add, commit an push their changes. You can jump onto the github website and verify that their changes have been pushed
- Now you should add commit and try and push your changes. You will get a message that looks like this:

  ```
  To https://github.com/skooter500/TestGit
   ! [rejected]        master -> master (non-fast-forward)
  error: failed to push some refs to 'https://github.com/skooter500/TestGit'
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  ```
- What this is saying is that there are changes on the server that you dont have and you need to pull and merge them before you can send your commit. To do this type:
- ```git pull```
- Now the changes from the head of the master branch on the server will get merged into your local git repository. git will attempt to merge files, but in this case you should get a merge conflict. It looks like this:

  ```
  Auto-merging TestGit/TestGit.pde
  CONFLICT (content): Merge conflict in TestGit/TestGit.pde
  Automatic merge failed; fix conflicts and then commit the result.
  ```
- If you open the file in question, you will see that it has been edited to look something like this:

  ```
  <<<<<<< HEAD
  // Hello from Bryan!
  =======
  // Hello from Tara!
  >>>>>>> c365e047b35d76bf3b2d48f38980db4b68746825

  void setup()
  {
  }
  ```
- The bits between <<<<<<< HEAD and ======= are the changes from your commit and the changes between ======= and >>>>>>> c365e047b35d76bf3b2d48f38980db4b68746825 are the changes from your team mates commit. Decide which bit you want to keep and delete the unwanted bits from the file and then add, commit and push your changes.

Merge conflicts on binary files
- Git can merge text files, with source code, but it cant merge binary files such as images. Lets see how to handle this
- Add an image to your project and have your team mate, commit and push this change.
- Have your team mate pull the repo to get the image.
- Now you should both have the image. Both of you should edit the image and save the changes
- Both you and your team mate should add and commit this change, but have your team mate push first
- When you try to push, you will get a message saying that your push has been rejected and you need to do a pull first

  ```
  To https://github.com/skooter500/TestGit
   ! [rejected]        master -> master (fetch first)
  error: failed to push some refs to 'https://github.com/skooter500/TestGit'
  hint: Updates were rejected because the remote contains work that you do
  hint: not have locally. This is usually caused by another repository pushing
  hint: to the same ref. You may want to first integrate the remote changes
  hint: (e.g., 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  ```

- When you do a pull, you will get a merge conflict on the image file:

  ```
  From https://github.com/skooter500/TestGit
     c365e04..43b59e5  master     -> origin/master
  warning: Cannot merge binary files: TestGit/test.JPG (HEAD vs. 43b59e5d2c53c909fb227a02b6e65681fa91e42a)
  Auto-merging TestGit/test.JPG
  CONFLICT (content): Merge conflict in TestGit/test.JPG
  Automatic merge failed; fix conflicts and then commit the result.

  ```
- git doesn't know how to deal with these edits and so to resolve this conflict, you have to decide which version of the file you want to keep, the one from the server, or your version. If you want to keep your version, you type:
  - ```git checkout --ours THE_FILE_NAME```
  - Don't forget to use / to seperate paths and use TAB to complete commands
  - If you want to keep the version from the server you can type
  - ```git checkout --theirs THE_FILE_NAME```
  - You can type these commands multiple times if you want to just swicth between the two versions to compare them.
- When you are done, add, commit and push your changes

Congratulations! I suggest you finish the lab by setting your assignment up on git

# Week 6
- [Irish economic data lab test from 2015](https://github.com/skooter500/irishEconomy/)
- [Politicians expenses lab test from 2014](processing/ExpensesProcessing)

- Video about map, ArrayList's, splitting strings, converting String to float:

[![YouTube](http://img.youtube.com/vi/jMC_y9Nhq04/0.jpg)](https://www.youtube.com/watch?v=jMC_y9Nhq04)

- Datasets in processing video:

[![YouTube](http://img.youtube.com/vi/ccnjXlSnL2Y/0.jpg)](https://www.youtube.com/watch?v=ccnjXlSnL2Y)

- [The expenses program we wrote in class](processing\expenses)

## Lab

### Learning Outcomes
- Create classes & objects
- Practice using an ArrayList
- Get experience loading data from a file
- Practice useful stuff for the upcoming lab test

Here is [the lab test document](docs/Lab Test 1.docx). You can attempt the entire test but dont worry if you can't figure out the party expenses part. What would be good to get done today would be the following:

- Create an ArrayList for Expense objects. Here is the [Processing reference for the ArrayList](https://processing.org/reference/ArrayList.html). Also [here is the example we wrote in the class today](processing/expenses).
- Load the expense data from the file into the ArrayList of Expense objects. You can use the processing method [loadTable](https://processing.org/reference/loadTable_.html) to do this. *Read the processing reference page for this carefully!!*
- Draw a barchart of the barchart of Expense objects.

Share your work on the Slack! Do the MCQ

# Week 5
- [Incomplete Game of Life code for the lab today](processing/lifeIncomplete)

- Stephen Hawkings on the Game of Life:

  [![YouTube](http://img.youtube.com/vi/CgOcEZinQ2I/0.jpg)](https://www.youtube.com/watch?v=CgOcEZinQ2I)

- John Conway on the Game of Life:

  [![YouTube](http://img.youtube.com/vi/C2vgICfQawE/0.jpg)](https://www.youtube.com/watch?v=C2vgICfQawE)

- Epic Conway's Game of Life:

  [![YouTube](http://img.youtube.com/vi/FdMzngWchDk/0.jpg)](https://www.youtube.com/watch?v=FdMzngWchDk)

- And finally, Alan Watts

  [![YouTube](http://img.youtube.com/vi/wU0PYcCsL6o/0.jpg)](https://www.youtube.com/watch?v=wU0PYcCsL6o)

- [Conway's Game of Life on Wikipedia](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)
- [The Game of Life Wiki](http://www.conwaylife.com/wiki/Main_Page)

## Lab
### Learning Outcomes
- Complete the game of life code
- Practice iterating over a 2D array
- Discover the amazing power of cellular automata

Try and complete the Game of Life we started in the class today. Here is the [code from the class](processing/lifeIncomplete).  you weren't in the class, you could take a read of the Game of Life wiki page and have a crack at implementing it from scratch yourselves. It's not too difficult. If you get your basic game of life to evolve, you could try these additions:

- The method ```void mousePressed()``` gets called in your sketch whenever the mouse is pressed. The method ```mouseDragged``` gets called whenever you hold the mouse down and move it over your sketch. You can get the mouse x and y coordinates by using the built in variables ```mouseX``` and ```mouseY```. You can use these methods to implement mouse drawing. To do this you need to calculate which row and column in the 2D array the mouse is over and then set this cell to be true.

- When you press the space key, the game should pause and unmpause, in other words, not update the game board while the game is paused
- When you press the c key, the board should clear. In otherwords, you should set every element in th 2D array to be false.
- When you press the r key, you should randomly set 50% of the elements to be true. To do this, you need to iterate through the array and generate a random number between 0.0f and 1.0f. If the number is > 0.5f, you set the element to be true otherwise set it to be false.

There some interesting starting patterns you can program also. You could write code so that when you press a number key it creates the starting pattern at the mouse x and y. I used the mouse x and y to be the top left of the shape.

| Pattern | Description |
|---------|-------------|
|![Sketch](images/p13.png) | Gosper Gun |
|![Sketch](images/p14.png) | Lightweight spaceship |
|![Sketch](images/p15.png) | Tumbler |
|![Sketch](images/p16.png) | Glider |
|![Sketch](images/p17.png) | I'm not sure what this is called, but it makes amazing patterns |

Here is a video of what my sketch looks like:

[![YouTube](http://img.youtube.com/vi/72X38iT74As/0.jpg)](https://www.youtube.com/watch?v=72X38iT74As)

Please share your work on the class slack and don't forget to do the MCQ this week.

- [A solution](processing/Life)
- [A solution that uses classes](processing/ProcessingLife)

# Week 4
- [The arrays program we wrote in the class](processing/arrays)
- [Arrays in Processing reference](https://processing.org/reference/Array.html)

- Arrays in processing - the basics

[![YouTube](http://img.youtube.com/vi/cMWxN4j30A0/0.jpg)](https://www.youtube.com/watch?v=cMWxN4j30A0)

- A video from last year about arrays in Processing

  [![YouTube](http://img.youtube.com/vi/ccnjXlSnL2Y/0.jpg)](https://www.youtube.com/watch?v=ccnjXlSnL2Y)

- Making the trend line:

  [![YouTube](http://img.youtube.com/vi/K9R5yQCPXIE/0.jpg)](https://www.youtube.com/watch?v=K9R5yQCPXIE)


## Lab

### Learning outcomes
- Practice iterating over arrays in Java
- Practice in using the for loop and variables to generate sequences of numbers
- Understand how a line graph is made
- Practice constructing alogorithms as part of a system
- Practice presenting data visually

Log into the slack and let me know how you are getting on today!

Use the code you wrote yesterday in the class as starter code for today's lab.
If you missed the class, [this is a link to my version](processing/arrays).

Here is what you can try and make today:

![Sketch](images/p7.png)

These are the steps I suggest you follow:

- Figure out how to draw a trend line graph first
- Then figure out how to leave horizontal and vertical borders around the graph. I would suggest making a variable called border to control this.
- Then figure out how to scale it so that it scales the data when drawing to the range 0-150. You could make this a variable
- Then figure out how to draw the horizontal axis. This will be a for loop obviously. You might find the following Java/Processing methods useful:
  - [The Processing map method](https://processing.org/reference/map_.html)
  - [textAlign](https://processing.org/reference/textAlign_.html)
  - [substring](http://www.tutorialspoint.com/java/java_string_substring.htm)
- Finally figure out how to draw the vertical axis. Another loop! This is the trickiest part I think

Try and parameterise as much of your sketch with variables, so that you could reuse the code to graph other types of data.
For example, I found it useful to write a method:

```Java
void drawAxis(float[] data, String[] horizLabels, int verticalIntervals, int maxVertical, float border)
```

to draw the horizontal and vertical axes. You might like to write seperate methods for the horizontal and vertical axis.
This took me about an hour to complete today, so it's tricky enough to get everything working, but worth it!
Take a screenshot of your sketch and [upload it to the slack](http://dt228-oop-2015.slack.com)!

### Advanced!

Try and draw this pie chart:

![Sketch](images/p8.png)

Upload screenshots of your sketches to Slack and log on to webcourses to do today's MCQ.

- [Solution to the lab](processing/data)

# Week 3
## Lecture
- [Trigonometry problem set](http://www.tippcityschools.com/cms/lib6/OH01000855/Centricity/Domain/111/Acc%20Geom%20eDay%201.pdf)
- [Simple Spirals sketch](processing/spiral)
- [Trigonometry problem visualised in processing](processing/kitetriangle)
- [Psychedelic Spirals sketch](https://github.com/skooter500/psychedelicSpirals)
- [Circles explained](https://www.khanacademy.org/math/trigonometry/unit-circle-trig-func/unit-circle-definition-of-trig-functions/v/unit-circle-definition-of-trig-functions-1)

Some interesting videos about generative art:

[![YouTube](http://img.youtube.com/vi/LaarVR1AOvs/0.jpg)](https://www.youtube.com/watch?v=LaarVR1AOvs)

[![YouTube](http://img.youtube.com/vi/x0OK1GiI83s/0.jpg)](https://www.youtube.com/watch?v=x0OK1GiI83s)

# Lab

## Learning outcomes

- Use variables
- Use for loops
- Use methods
- Construct an algorithm to solve a problem using sin, cos and the unit circle
- Use drawing and colours in a Processing sketch
- Use random numbers
- Be creative with code

In the lecture we learned how to make spiral shapes using a for loop with sin and cos. In the lab today you will make a sketch that draws star shapes with random numbers of points and random colours. Here is what the finished sketch could look like:

![Sketch](images/p5.png)

Here are some things you might need to read up on first:

- [random function in Processing](https://processing.org/reference/random_.html)
- [Using the modulus operator](http://www.cafeaulait.org/course/week2/15.html)

You can put all your code into the setup method as this sketch doesn't use any animation (unles you want to attempt the advanced part)

This is how I suggest you think about the problem.

- You will need a for loop that goes from 0 - TWO_PI. There will be twice as many steps as there are points on the star.
- You can use % (modulus) to decide whether the x and y values you calculate should be the tip of a point or base of the point (the pointy bit or the trough).
- Use line in your solution
- I strongly suggest you start the lab by just drawing a single star and then maybe move on to drawing multiple stars using a for loop.
- You could write a methdod to draw a single star with parameters

### Advanced
- Make a beautiful animated sketch with stars and spirals and share a picture/video/animated gif on the slack
- Use sin and cos to control colours

Do MCQ 2 and MCQ 3

- [Solution to the lab](processing\star)

## Tutorial
- [My generartive art project](https://github.com/skooter500/genart1)

# Week 2
## Lecture
- [Quadrants sketch](processing/quadrants) - How to use the if statement
- [Rectangle sketch](processing/rectangle) - Rectangle moves back and forth across the screen
- [Examples of using loops in Processing](processing/loops)
- [Solution to the BugZap lab](https://github.com/skooter500/BugZap)

* Data types, the if statement and dynamic sketches in Processing video (from last year)

  [![YouTube](http://img.youtube.com/vi/Y0b9W3UJ2BU/0.jpg)](https://www.youtube.com/watch?v=Y0b9W3UJ2BU)

# Lab
## Learning Outcomes
- Use what you learned in class to build a complete game system in Processing
- Practice drawing stuff and working out relative co-ordinates
- Practice using variables and compound if statements
- Gain experience thinking computationally
- Learn how to use random numbers
- Learn how to get input from the keyboard
- Learn how to import libraries into Processing

This is a video of a game called Bugzap that you can try and make in Processing today. There is a fair bit to it, so don't worry if you don't manage to complete everything.

[![YouTube](http://img.youtube.com/vi/s6PA8jtWneQ/0.jpg)](https://www.youtube.com/watch?v=s6PA8jtWneQ)

How you should do it:
- Get the main game working first and then if you have time, add fonts, sound, the splash screen and the game over screen.
- Write some code to draw the bug. You can write a method to do this if you like (but it's not essential). Here is [an article on using methods in processing](https://processing.org/examples/functions.html). Also make global variables for the bug position and size.
- Get the bug moving. The bug moves a random amount either to the left or the right and it also moves down the screen. Use the random method in Processing to generate random numbers. Also the bug can't move off the screen. You can use the % operator to make something happen on an interval. For example:

  ```Java
  if (frameCount % 60 == 0)
  {
    // Code in here will happen once per second
  }
  ```
- Write some code to draw the player. Use variables to control the player position and size. A method is good here too!
- Write code to move the player in response to a key presses. This is one way to do keyboard handling in Processing:

```Java
if (keyPressed)
{
  if (keyCode == LEFT)
  {
    // This will happen if the left key is pressed
  }
}
```
- Now add the player lazer. I used to UP key for this. I just drew a line for the lazer.
- Make a variable for score and check for collisions between the lazer and the bug. Add a variable for score. You can print stuff to the screen using the text method in Processing. In my version, I actually used [this processing library](http://www.foobarquarium.de/blog/processing/MovingLetters/) which makes wireframe text.
- Make some sound effects and add them to the game. I used [BFXR](http://www.bfxr.net/) to make the sounds and the Minim library to play them, but you might prefer to use the [built-in audio methods in Processing](https://processing.org/tutorials/sound/).
- Add the splash screen and game over screen

Upload pictures of your creations to the Slack and do this weeks MCQ.

# Week 1

## Lecture
* [Introduction slides](https://1drv.ms/p/s!Ak7y2552PWCrhONjAgskv4PATGqdpw)
* [The contract for this course](https://1drv.ms/w/s!Ak7y2552PWCrjPYXt8HlWl1T1cg5Og)

## Lab

### Learning Outcomes
- Sign up for the class Slack
- Enroll on Webcourses
- Become familiar with the syntax of Processing
- Become familiar with writing and running sketches in Processing

Firstly, go to https://oop-2016-2017.slack.com and sign up for the slack with your DIT email address. Make sure and click *Create an account* rather than try and enter your DIT credentials at the login screen, which wont work. When you are signed up, send a little greeting to everyone on the #general channel. If you have a smartphone, you might want to install the Slack app. It's free. Also if you install the app, you will probably want to disable certain notifications, otherwise your phone will be buzzing every time someone posts anything. [Here is an article that explains how to do this](https://slack.zendesk.com/hc/en-us/articles/201649323-Channel-and-group-notification-preferences).

Log onto Webcourses and enroll on the module CMPU2016.

Look up the following methods in the [Processing language reference](http://processing.org/reference/ ) to make sure you are clear about the syntax and parameters:

* noStroke
* noFill
* line
* ellipse
* rect
* background
* stroke
* fill
* size
* arc
* triangle

Write a processing sketch to draw the following shapes:

![Sketch](images/p1.png)

![Sketch](images/p1.1.png)

![Sketch](images/p1.2.png)

I prefer to draw the shapes on paper first before I try and work out the coordinates. Try experimenting with different colours

[Log onto webcourses](http://dit.ie/webcourses) and do this weeks MCQ.