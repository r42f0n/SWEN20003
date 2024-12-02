java cSWEN20003 Object Oriented Software Development Project 1, 2024
The University of Melbourne
School of Computing and Information Systems
SWEN20003 Object Oriented Software Development
Project 1, Semester 2, 2024
Released: Friday, 23rd August 2024 at 4:00pm AEST
Initial Submission Due: Wednesday, 28th August 2024 at 4:00pm AEST
Project Due: Wednesday, 4th September 2024 at 4:00pm AEST
Please read the complete specification before starting on the project, because there
are important instructions through to the end!
Overview
Welcome to the first project for SWEN20003, Semester 2, 2024. Across Project 1 and 2, you
will design and create a taxi simulation game in Java called ShadowTaxi. In Project 1, you will
create the first part of the full game that you will complete in Project 2B. This is an individual
project. You may discuss it with other students, but all of the implementation must be your
own work. By submitting the project you declare that you understand the University’s policy on
academic integrity and aware of consequences of any infringement, including the use of artificial
intelligence.
You may use any platform and tools you wish to develop the game, but we recommend using IntelliJ
IDEA for Java development as this is what we will support in class.
The purpose of this project is to:
 Give you experience working with an object-oriented programming language (Java),
 Introduce simple game programming concepts (2D graphics, input, simple calculations)
 Give you experience working with a simple external library (Bagel)
Extensions  Special Considerations: From Semester 2, 2024, The Faculty of Engineering
and Information Technology has a new process in place for handling Extensions and Special Con-
siderations, linked here. Carefully read through the instructions about the same. This information
is also published in Canvas -> Modules -> FEIT Extensions and Special Consideration. Do not
send emails to the Subject Coordinator without reviewing this process first.
Late Submissions: If you submit late (either with or without an extension), please complete the
Late form in the Projects module on Canvas. For the form, you need to be logged in using your
university account. Please do not email any of the teaching team regarding late submissions. All
of this is explained again in more detail at the end of this specification.
You must make at least 5 commits (excluding the Initial Submission commit) throughout the
development of the project, and they must have meaningful messages. This is also explained in
more detail at the end of the specification.
1
SWEN20003 Object Oriented Software Development Project 1, 2024
Game Overview
“You are a taxi driver stuck on an endless road, attempting to survive in this current economic
crisis. Move the taxi in the lanes, pick up passengers and drop off the passengers at their trip
end flags to earn money. Each passenger has a priority, which can increase the driver’s earnings.
Collect the coins, to increase the passenger’s priority. If you stop past the trip end flag, you lose
money! Can you beat the target score before the time elapses to complete the game?
Project 1 features only the first part of the full game, as described above. The player has to
press the arrow keys to move the taxi left, right or up. The taxi can pick up one passenger at a
time, by stopping close to them. The taxi can collect coins by colliding with them - collecting coins
will increase the priority of the current passenger once. The player has to drop the passenger off
at their respective trip end flag - stopping past this flag, incurs a penalty on the earnings of that
trip. Once dropped off, the trip earnings are added to the total score. To win, the player needs to
beat the target score of 500. If the game runs for more than 15,000 frames, the game ends in a
loss. At the end, the current top 5 scores are shown on screen.
Figure 1: Completed in-game Project 1 screenshot
2
SWEN20003 Object Oriented Software Development Project 1, 2024
The Game Engine
The Basic Academic Game Engine Library (Bagel) is a game engine that you will use to develop
your game. You can find the documentation for Bagel on Canvas under the Projects module.
Coordinates
Every coordinate on the screen is described by an (x, y) pair. (0, 0) represents the top-left of the
screen, and coordinates increase towards the bottom-right. Each of these coordinates is called a
pixel. The Bagel Point class encapsulates this.
Frames
Bagel will refresh the program’s logic at the same refresh rate as your monitor. Each time, the
screen will be cleared to a blank state and all of the graphics are drawn again. Each of these steps
is called a frame. Every time a frame is to be rendered, the update() method in ShadowTaxi is
called. It is in this method that you are expected to update the state of the game.
The refresh rate is typically 120 times per second (Hz) but some devices might have a lower rate
of 60Hz. In this case, when your game is running, it may look different to the demo videos as
the constant values in this specification have been chosen for a refresh rate of 120Hz. For your
convenience, when writing and testing your code, you may change these values to make your game
playable. If you do change the values, remember to change them back to the original specification
values before submitting.
The Game Elements
The default window size should be 1024 * 768 pixels. The game consists of a few screens and
other different game elements. Below is an outline of these elements you will need to implement.
Home Screen
This is the first screen rendered when the game is started. The background (backgroundHome.png)
should be rendered on the screen and completely fill up your window during this screen. This has
already been implemented for you in the skeleton package.
A title message that reads SHADOW TAXI should be rendered with the font provided in the res
folder (FSO8BITR.ttf), with a font size 64. The bottom left of the message should be calculated
as follows: the x-coordinate should be centered horizontally and the y-coordinate should be at 384
pixels.
Below this, an instruction message that reads PRESS ENTER should be rendered in the provided font,
in size 32. The x-coordinate of the bottom left of the message should be centered horizontally, and
the y-coordinate should be at 500 pixels. When the Enter key is pressed, the game changes to the
Player Information Screen.
3
SWEN20003 Object Oriented Software Development Project 1, 2024
Hint: The drawString() method in the Font class uses the given coordinates as the bottom left
of the message. So to center the message, you will need to calculate the coordinates using the
Window.getWidth() and Font.getWidth() methods.
Player Information Screen
The background (backgroundPlayerInfo.png) should be rendered on the screen and completely
fill up your window during this screen. All messages on this screen are in the provided font, in size
24. The x-coordinate of the bottom left of all the messages should be centered horizontally.
An instruction message that reads ENTER YOUR NAME should be rendered at the top. The y-
coordinate of the bottom left of this message should be at 200 pixels.
When the user types their name, the entered letters needs to be rendered in black in the white box
on this screen. When the user presses the Backspace or Delete key, the last letter of the currently
rendered name needs to be removed. The y-coordinate of the bottom left of this name should
be at 380 pixels. Hint: The DrawOptions class in Bagel will help you change the colour of the
text. There is also a method given to you in the skeleton that will convert a key press into the
corresponding String value.
Additionally, an instruction message consisting of 2 lines:
PRESS ENTER TO START
USE ARROW KEYS TO MOVE
should be rendered below the white box. The y-coordinate of the bottom left of this message should
be at 500 pixels. There must be adequate spacing between the 2 lines to ensure readability (you
can decide on the value of this spacing yourself, as long as it’s not small enough that the text
overlaps or too big that it doesn’t fit within the screen). When the Enter key is pressed, the game
changes to the Game Play Screen.
Game Play Screen
This screen features two backgrounds stacked vertically in the y-axis, to create a scrolling effect
during game play. For each background, the same image background.png must be used. The
starting centre coordinates of the first background is (512, 384) and for the second, (512, -384).
The second background starts above the first, initally off-screen (these values are in fact, half the
default window width and window height).
When the player presses the up arrow key, both backgrounds move vertically down by a speed of
5 pixels per frame. If the current y-coordinate of the centre of one background becomes greater
than or equal to 1152, the y-coordinate is set to the (y-coordinate of other background) -
Window.getHeight(). In other words, the background leaving past the bottom of the window,
moves to above the window (if done correctly, this will look like a scrolling effect and the taxi
moves up on an endless road).
The game entities and the actual game play will happen during this screen. This behaviour is
explained in detail later in the Game Entities section.
4
SWEN20003 Object Oriented Software Development Project 1, 2024
Game End Screen
When the player wins or loses, the player’s name and score (separated by a comma) needs to be
written into the res/scores.csv file. A method to write to the comma-separated value (CSV) file
is given to you in the skeleton package.
For a win or a loss, the game changes to this screen. The background (backgroundEnd.png) should
be rendered on the screen and completely fill up your window during this screen. All messages on
this screen are in the provided font. The x-coordinate of the bottom left of all the messages should
be centered horizontally.
On this screen, a message that reads "TOP 5 SCORES -" should be rendered at the top, with a
font size of 20. The y-coordinate of the bottom left of this message should be at 200 pixels.
Below this, the top five scores currently stored in the CSV file, have to be rendered. If there are
less than five, all scores will be shown. Each line will be in the format of "i - j", where i is the
player name and j is the score, given to 2 decimal places. The bottom left of each line should be
calculated as follows: the x-coordinate will be centered horizontally and the y-coordinate increases
by 40 from 200 pixels (i.e the bottom of the scoring message described above).
A method to read the CSV file and return the Strings, is given to you in the skeleton package (you
will need to choose the top 5 scores before rendering however).
If the player beats the target score of 500, this is considered as a win. A message should be
rendered, that consists of 2 lines:
CONGRATULATIONS, YOU WON!
PRESS SPACE TO CONTINUE
If the game runs for more than 15,000 frames without a win happening, this is considered as a
loss and the game ends. In this case, the message should be rendered as:
GAME OVER, YOU LOST!
PRESS SPACE TO CONTINUE
The win/loss message should be rendered, in the font provided, in size 24. The y-coordinate should
be at 500 pixels.
If the Space key is pressed, the game returns to the Home Screen and allows the player to play
again. If the player terminates the game window at any point (by pressing the Escape key or by
clicking the Exit button), the window will simply close and no message will be shown.
5
SWEN20003 Object Oriented Software Development Project 1, 2024
(a) Home Screen (b) Player Information Screen (c) Game End Screen
Figure 2: Game Screens (Game Play Screen is shown in Figure 1)
Properties File
The key values of the game are listed in two properties files which are given in the skeleton pack-
age. The message coordinates, image filenames and other values are given in the app.properties
file. The message strings are given in the message en.properties file. These files shouldn’t be
edited (unless you need to adjust values for any frame rate issues).
To read a value from one of these properties, a Properties object must be created. The
getProperty method can be called on this object with the required value given as the param-
eter. For your reference, the skeleton package contains an example of how to read the background
image filename, window width and window height values.
World File
The entities will be defined in a world file, describing the type and their position in the window.
The world file is located at res/gameObjects.csv. A world file is a comma-separated value (CSV)
file with rows in one of the following formats:
TAXI or COIN, x-coordinate, y-coordinate
or
PASSENGER, x-coordinate, y-coordinate, priority, end x-coordinate, y-distance
An example of a world file is shown below:
TAXI,500,600
COIN,450,-316
COIN,309,-2167
PASSENGER,280,-800,3,280,500
PASSENGER,280,-1500,1,700,800
The given (x, y) coordinates refer to the centre of each image and these coordinates should be
used to draw each image. For each passenger, the end x-coordinate is for the end of their trip and
6
SWEN20003 Object Oriented Software Development Project 1, 2024
the y-distance is the distance travelled vertically during the trip. The priority is explained later in
the Passenger section.
You must actually load the file—copying and pasting the data, for example, is not allowed. Marking
will be conducted on a hidden different CSV file of the same format. You have been given a method
to read a CSV file in the skeleton package. Note: The values in the example may not be the
same as the ones given to you and the order of the entities may change.You can assume that there
will always be at least one of each for all the entities. You can also assume there is only taxi for
Project 1.
Game Entities
The following game entities have an associated image and a starting location (x, y). Remember
that all images are drawn from the centre of the image using these coordinates. Each entity has
behaviour that interacts with the other entities, so make sure you read this section fully, before you
ask any questions on Ed Discussions!
Taxi
Figure 3: taxi.png
The taxi is represented by the image taxi.png, shown on the left. It
has a radius value of 32. In our game, the taxi can move on screen in
one of three directions (left, right and up) when the corresponding arrow
key is pressed. However, for our ease of implementation, we assume the
taxi can only move horizontally and remains stationary in the vertical
direction (i.e. the other entities will be moving in relation to the player’s
arrow keys pressed - this is explained for each entity later).
Hence, when the player’s right arrow key is pressed or held down, the taxi will move to the right
by 1 pixel per frame. When the player’s left arrow key is pressed or held down, the taxi will
move to the left by the same speed.
Figure 4: Taxi’s score,
target  frames render-
ing
When the taxi picks up a passenger, the taxi will have an associated
trip. The taxi also has an associated total score. Once a trip is com-
plete, the earnings of that trip is added to the total score. The trip
earnings calculation is explained later in the Trip section. The total
score is rendered in the top left corner of the screen in the format of
"PAY k" where k is the current total score, shown to 2 decimal places.
The bottom left corner of this message should be located at (35, 35)
and the font size should be 20.
The target score of 500.00, should also be rendered on screen, in the
format of "TARGET k", where k is the t代 写SWEN20003、Java
代做程序编程语言arget score. The bottom left corner of this message should
be located at (10, 65) and the font size should be 20.
The remaining number of frames is shown on screen in the format of "FRAMES REM k", where k is
the number of frames remaining. The bottom left corner of this message should be located at (10,
95) and the font size is again 20.
7
SWEN20003 Object Oriented Software Development Project 1, 2024
Passenger
Figure 5: passen-
ger.png
A passenger is an entity shown by passenger.png. When the player’s up
arrow key is pressed or held down, the passenger will move vertically down
by 5 pixels per frame.
A passenger has an associated priority value of 1, 2 or 3, where 1 is the
highest priority. The higher the priority, the higher the trip earnings -
this is explained in detail later. The priority is rendered only when the
passenger has not been picked up yet. It is shown as an integer, at the
coordinates of (x - 30, y) where x and y are the current coordinates of the passenger. The font
size should be 12.
The expected earnings for each passenger before being picked up by the taxi, will be rendered
on screen. It is shown to 1 decimal place, at the coordinates of (x - 100, y) where x and y are
the current coordinates of the passenger. The font size is 12. The details of how to calculate the
earnings are explained later in the Trip section.
For the taxi to pick up a passenger, three conditions must be fulfilled -
 the taxi must be stopped, i.e. not moving in the horizontal or vertical direction.
 the taxi has no current passenger.
 the taxi must be adjacent to the passenger. This is calculated by calculating the Euclidean
distance between the two (x, y) coordinates of the taxi and passenger. If this current
distance is less than or equal to 100, this is considered as adjacent.
If all 3 conditions are true, the passenger will move towards the taxi. The passenger’s (x, y)
coordinates will increase or decrease respectively, by 1 pixel per frame, until the Euclidean
distance between the coordinates and the taxi’s current coordinates is less than or equal to 1. (for
ease, you may consider this motion as two separate movements, in the x and y directions).
Once the passenger is picked up, the trip will commence and the taxi will move based on the
user’s input as described in the Taxi section. During this movement, the passenger’s image will
not be rendered - only the taxi image will be shown. However, the passenger’s coordinates will
need to be updated whenever the taxi’s coordinates are updated.
When the trip is complete, the passenger will leave the taxi. This happens when the first condition
and either of the second or third conditions are met -
 the taxi must be stopped, i.e. not moving in the horizontal or vertical direction.
 the taxi’s y-coordinate must be less than or equal to the y-coordinate of the trip end flag
(i.e. the taxi has just moved above the end flag on screen).
OR
 the distance between the taxi’s coordinates and the trip end flag’s coordinates, is less than
or equal to the radius of the trip end flag, which has a value of 80 (i.e. the taxi has stopped
in the radius of the end flag).
8
SWEN20003 Object Oriented Software Development Project 1, 2024
If this is satisfied, the passenger will leave the taxi and move towards the trip end flag. The pas-
senger’s (x, y) coordinates will increase or decrease respectively, by 1 pixel per frame again,
until the coordinates match the trip end flag’s coordinates (for ease, you may consider this motion
as two separate movements, in the x and y directions). Once the passenger’s coordinates are equal
to the trip end flag’s coordinates, the passenger’s image will stay at that position.
Trip End Flag
Figure 6: tripEnd-
Flag.png
A trip end flag is an entity shown by tripEndFlag.png and has a radius
value of 80. When the player’s up arrow key is pressed or held down,
the flag will move vertically down by 5 pixels per frame. The flag’s x-
coordinate is the passenger’s end x-coordinate, given in the world file. The
flag’s y-coordinate needs to be calculated using the passenger’s starting y-
coordinate and y-distance to travel during the trip, both given in the world file (remember that
y-coordinates decrease when moving vertically up on screen!)
Once a passenger has been picked up (i.e. a trip has started), the flag will be rendered on screen.
As described in the previous section, the trip end flag’s radius and coordinates are used in the
check for when the trip is complete. Once the passenger reaches the trip end flag, it is no longer
rendered on screen.
Coin
Figure 7: coin.png
A coin is an entity shown by coin.png and has a radius value of 20.
When the player’s up arrow key is pressed or held down, the coin will
move vertically down by 5 pixels per frame.
When a coin collides with the taxi, the taxi gains the coin power for 500
frames. If the taxi either has a passenger before collision or picks up a passenger whilst the coin
power is active, the passenger’s current priority value is decreased by 1 (i.e. passenger gains
higher priority).
To determine if the coin has collided with the taxi, a range is first calculated by adding the radius
of the coin image and the radius of the taxi image. The current distance between the two (x, y)
coordinates of the taxi and coin, is calculated. If the current distance is less than or equal to
the range, this is considered as a collision. Once collided with, the coin is no longer rendered on
screen.
A taxi can collide with multiple coins during a trip but the passenger’s priority will increase only
once. If the passenger’s current priority value is already 1, nothing will happen. The number of
frames that the (most recently collided with) coin has been active for is rendered on the screen
as an integer. The bottom left corner of this message should be located at (900, 35) and the font
size should be 20. This means that every time a new coin is collided with, the rendered frame count
”will look like” it has reset.
9
SWEN20003 Object Oriented Software Development Project 1, 2024
Trip
A trip is not a single entity shown on screen - it is included here to help explain the earnings
calculation and message rendering. The earnings are calculated when a trip is complete (based
on the conditions described in the Passenger section). The earnings are calculated as the sum of
two fees - distance fee and priority fee.
The distance fee is calculated by multiplying the y-distance travelled with the rate per y-distance
of 0.1. The priority fee is calculated by multiplying the passenger’s current priority value with
the priority rate. The priority rates are given in the below table.
Priority Rate
1 50
2 20
3 10
For example :-
 A passenger of initial priority 3, has travelled for 50 pixels. The distance fee would be 50 x
0.1 = 5. The priority fee would be 3 x 10 = 30. The total earnings would be 5 + 30 = 35.
 A passenger of initial priority 3, has travelled for 150 pixels and the taxi has collided with
one coin. The distance fee would be 150 x 0.1 = 15. The priority fee would be 2 x 20 = 40.
The total earnings would be 15 + 40 = 55.
A penalty will be applied if three conditions are met -
 the taxi is stopped, i.e. not moving in the horizontal or vertical direction.
 the taxi’s y-coordinate must be less than the y-coordinate of the trip end flag (i.e. the taxi
has moved beyond the trip end flag on screen).
 the distance between the taxi’s coordinates and the trip end flag’s coordinates, is greater
than the radius of the trip end flag.
The penalty is calculated by multiplying the penalty rate of 0.05 with the distance between the trip
end flag’s y-coordinate and the taxi’s y-coordinate when it stopped (when the trip was completed).
The penalty will be subtracted from the trip earnings. If the earnings becomes negative, it will
be set to 0. (What this implies is that, a ”perfect” trip ending will be with the taxi stopping as close
as possible to the trip end flag).
As mentioned earlier in the Passenger section, the expected trip earnings are rendered on screen
next to each passenger before being picked up - this will not include any penalties as the trip has
not yet started.
Once the trip commences, the trip details are shown on screen in the bottom left. The font sizes
for all of these details are 20 and the x-coordinate of bottom left corner of each message should
be located at 35. First, a message that reads "CURRENT TRIP -" is rendered with the bottom left
y-coordinate at 650. 30 pixels below this, the expected earnings are rendered in the format of "EXP
FEE k", where k is the current expected earnings, given to 1 decimal place. 60 pixels below the
first trip message, the passenger’s current priority value is rendered in the format of "PRIORITY
10
SWEN20003 Object Oriented Software Development Project 1, 2024
k", where k is the current priority value, as an integer. Remember that current priority values (and
expected earnings) can change if a coin has been collided with!
Once the trip is complete, the first trip message is replaced by one that reads "LAST TRIP -" in
the same position as before. The penalty value is shown 90 pixels below the first trip message, in
the format of "PENALTY k", where k is the penalty value, shown to 2 decimal places. The penalty
value is shown even if there is no penalty for that trip. The trip earnings (with any possible
penalties) are added to the total score, which will be updated. These last trip details will continue
to be rendered until a new trip commences.
(a) Current Trip (b) Last Trip
Figure 8: Sample Trip Detail Rendering
Your Code
You must submit a class called ShadowTaxi that contains a main method that runs the game as
prescribed above. You may choose to create as many additional classes as you see fit, keeping in
mind the principles of object oriented design discussed so far in the subject. The purpose of this
project is to evaluate how well you use OOSD concepts, specifically classes. Project 2 will require
use of more advanced OOSD concepts. You will be assessed based on your code running correctly, as
well as the effective use of Java concepts. As always in software engineering, appropriate comments
and variables/method/class names are important.
Implementation Checklist
To get you started, here is a checklist of the game features, with a suggested order for implementing
them:
 Draw the home screen and the messages
 Draw the player information screen and the messages
 Draw the game play screen
 Read the world file, then draw the taxi, one coin and one passenger on screen
 Implement vertical movement logic for the 3 entities above
 Implement image rendering and vertical movement for all the entities in the world file
 Implement the passenger pick up and drop off movement
11
SWEN20003 Object Oriented Software Development Project 1, 2024
 Implement the trip earnings calculation and total score rendering
 Implement the coin collision, effect on passenger priority  frame count rendering
 Implement win and loss detection
 Implement game end screen and top scores rendering
Supplied Package
You will be given a package called project-1-skeleton.zip that contains the following: (1)
Skeleton code for the ShadowTaxi and IOUtils classes to help you get started, stored in the src
folder. (2) All graphics, fonts and properties that you need to build the game, stored in the res
folder. (3). The pom.xml file required for Maven. Here is a more detailed description:
 res/ – The graphics and font for the game (you are not allowed to modify any of the files in
this folder).
– background.png: The image to represent the background for the Game Play screen
– backgroundEnd.png: The image to represent the background for the Game End screen
– backgroundHome.png: The image to represent the background for the Home screen
– backgroundPlayerInfo.png: The image to represent the background for the Player
Information screen
– coin.png: The image to represent a coin.
– passenger.png: The image to represent a passenger.
– taxi.png: The image to represent the taxi.
– tripEndFlag.png: The image to represent the end flag.
– app.properties: The properties file containing coordinates, values and file paths.
– message en.properties: The properties file containing the message strings.
– FSO8BITR.ttf: The font to be used throughout this game.
– gameObjects.csv: The world file for the game.
– scores.csv: The CSV file to store the scores.
– credit.txt: The file containing credit for the font and images (you can ignore this file).
 src/ – The skeleton code for the game.
– ShadowTaxi.java: The skeleton code that contains an entry point to the game and an
update() method that draws the Home Screen background.
– IOUtils.java: The skeleton code that has completed methods to read a CSV file, read
a Properties file and write to a CSV file.
12
SWEN20003 Object Oriented Software Development Project 1, 2024
– MiscUtils.java: The skeleton code that has a completed method to convert an input
key press into the corresponding String value.
 pom.xml: File required to set up Maven dependencies.
Submission and Marking
Initial Submission
To ensure you start the project with a correct set-up of your local and remote repository, you
must complete this Initial Submission procedure on or before Wednesday, 28th August 2024
at 4:00pm.
1. Clone the [user-name]-project-1 folder from GitLab.
2. Download the project-1-skeleton.zip package from Canvas, under Project 1.
3. Unzip it.
4. Move the contents of the unzipped folder to the [user-name]-project-1 folder in your
local machine.
5. Add, commit and push this change to your remote repository with the commit message
"initial submission".
6. Check that your push to Gitlab was successful and to the correct place.
After completing this, you can start implementing the project by adding code to meet the require-
ments of this specification. Please remember to add, commit and push your code regularly with
meaningful commit messages as you progress.
You must complete the Initial Submission following the above instructions by the due date. Not
doing this will incur a penalty of 3 marks for the project. It is best to do the Initial Submis-
sion before starting your project, so you can make regular commits and push to Gitlab since the
very start. However, if you start working on your project locally before completing Initial Sub-
mission, that is fine too, just make sure you move all of the contents from your project folder to
[user-name]-project-1 in your local machine.
Technical requirements
 The program must be written in the Java programming language.
 Comments and class names must be in English only.
 The program must not depend upon any libraries other than the Java standard library and
the Bagel library (as well as Bagel’s dependencies).
 The program must compile fully without errors.
Submission will take place through GitLab. You are to submit to your -project-1
repository. At the bare minimum you are expected to follow the structure below. You can create
more files/directories in your repository if you want. It is expected you will create additional classes
13
SWEN20003 Object Oriented Software Development Project 1, 2024
following good OOSD concepts. Marks are allocated towards suitable design, not just implemen-
tation.
username -project-1
res
resources used for project 1
src
ShadowTaxi.java
other Java files
On 4th September 2024 at 4:00pm, your latest commit will automatically be harvested from GitLab.
Commits
You are free to push to your repository post-deadline, but only the latest commit on or before 4th
Septembe         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
