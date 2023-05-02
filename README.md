Download Link: https://assignmentchef.com/product/solved-cmsc421-project-1-vehicle-route-finding
<br>
1

<h1>Problem domain</h1>

<ul>

 <li>Modified version of <a href="https://en.wikipedia.org/wiki/Racetrack_(game)">Racetrack </a>I Invented in early 1970s

  <ul>

   <li>played by hand on graph paper</li>

  </ul></li>

 <li>2-D polygonal region

  <ul>

   <li>Inside are a starting point, finish line, maybe obstacles</li>

  </ul></li>

 <li>All walls are straight lines</li>

 <li>All coordinates are nonnegative integers</li>

 <li>Robot vehicle begins at starting point, can make certain kinds of moves</li>

 <li>Want to move it to the finish line as quickly as possible I Without crashing into any walls

  <ul>

   <li>Need to come to a complete stop on the finish line</li>

  </ul></li>

</ul>

<h1>Moving the vehicle</h1>

<ul>

 <li>Before the <em>i</em>’th move, current state is <em>s</em><em>i</em>−1 = (<em>p</em><em>i</em>−1<em>,z</em><em>i</em>−1)

  <ul>

   <li>location <em>p</em><em>i</em>−1 = (<em>x</em><em>i</em>−1<em>,y</em><em>i</em>−1), nonnegative integers</li>

  </ul></li>

</ul>

I velocity <em>z</em><em>i</em>−1 = (<em>u</em><em>i</em>−1<em>,v</em><em>i</em>−1), integers

<ul>

 <li>To move the vehicle

  <ul>

   <li>First choose a new velocity <em>z<sub>i </sub></em>= (<em>u<sub>i</sub>,v<sub>i</sub></em>), where</li>

  </ul></li>

</ul>

<table width="622">

 <tbody>

  <tr>

   <td width="590"><em>u</em><em>i </em>∈{<em>u</em><em>i</em>−1 − 1<em>, u</em><em>i</em>−1<em>, u</em><em>i</em>−1 + 1}<em>,</em></td>

   <td width="32">(1)</td>

  </tr>

  <tr>

   <td width="590"><em>v</em><em>i </em>∈{<em>v</em><em>i</em>−1 − 1<em>, v</em><em>i</em>−1<em>, v</em><em>i</em>−1 + 1}<em>.</em></td>

   <td width="32">(2)</td>

  </tr>

 </tbody>

</table>

I New location:        <em>p<sub>i </sub></em>= (<em>x<sub>i</sub></em><sub>−1 </sub>+ <em>u<sub>i</sub>,y<sub>i</sub></em><sub>−1 </sub>+ <em>v<sub>i</sub></em>)

I New state:      <em>s<sub>i </sub></em>= (<em>p<sub>i</sub>,z<sub>i</sub></em>)

Example

<ul>

 <li>Initial state: <em>p</em><sub>0 </sub>= (4<em>,</em>5) <em>z</em><sub>0 </sub>= (0<em>,</em>0) <em>s</em><sub>0 </sub>= (<em>p</em><sub>0</sub><em>,z</em><sub>0</sub>) = ((4<em>,</em>5)<em>,</em>(0<em>,</em>0))</li>

 <li>First move:</li>

</ul>

<em>z</em><sub>1 </sub>= (0<em>,</em>0) + (1<em>,</em>1) = (1<em>,</em>1) <em>p</em><sub>1 </sub>= (4<em>,</em>5) + (1<em>,</em>1) = (5<em>,</em>6) <em>s</em><sub>1 </sub>= ((5<em>,</em>6)<em>, </em>(1<em>,</em>1))

<ul>

 <li>Second move:</li>

</ul>

<em>z</em><sub>2 </sub>= (1<em>,</em>1) + (−1<em>,</em>1) = (0<em>,</em>2) <em>p</em><sub>2 </sub>= (5<em>,</em>6) + (0<em>,</em>2) = (5<em>,</em>8) <em>s</em><sub>2 </sub>= ((5<em>,</em>8)<em>, </em>(0<em>,</em>2))

<ul>

 <li>Third move:</li>

</ul>

<em>z</em><sub>3 </sub>= (0<em>,</em>2) + (1<em>,</em>0) = (1<em>,</em>2) <em>p</em><sub>3 </sub>= (5<em>,</em>8) + (1<em>,</em>2) = (6<em>,</em>10) <em>s</em><sub>3 </sub>= ((6<em>,</em>10)<em>, </em>(1<em>,</em>2))

<h1>Walls</h1>

<ul>

 <li><em>edge</em>: a pair of points (<em>p,q</em>)</li>

</ul>

I <em>p </em>= (<em>x,y</em>), <em>q </em>= (<em>x</em><sup>0</sup><em>,y</em><sup>0</sup>)

<ul>

 <li>coordinates are nonnegative integers</li>

 <li><em>wall</em>: an edge that the vehicle can’t cross</li>

 <li>List of walls in the example:</li>

</ul>

[((0<em>,</em>0)<em>,</em>(10<em>,</em>0))<em>, </em>((10<em>,</em>0)<em>,</em>(10<em>,</em>10))<em>, </em>((10<em>,</em>10)<em>,</em>(20<em>,</em>10))<em>, </em>((20<em>,</em>10)<em>,</em>(30<em>,</em>0))<em>, </em>((30<em>,</em>0)<em>,</em>(30<em>,</em>10))<em>, </em>((30<em>,</em>10)<em>,</em>(10<em>,</em>20))<em>,</em>

((10<em>,</em>20)<em>,</em>(0<em>,</em>20))<em>,    </em>((0<em>,</em>20)<em>,</em>(0<em>,</em>0))<em>,      </em>((3<em>,</em>14)<em>,</em>(10<em>,</em>14))<em>,</em>

((10<em>,</em>14)<em>,</em>(10<em>,</em>16))<em>, </em>((10<em>,</em>16)<em>,</em>(3<em>,</em>16))<em>, </em>((3<em>,</em>16)<em>,</em>(3<em>,</em>14))]

<h1>Moves and paths</h1>

<ul>

 <li><em>move</em>: an edge <em>m </em>= (<em>p<sub>i</sub></em><sub>−1</sub><em>,p<sub>i</sub></em>)

  <ul>

   <li><em>p</em><em>i</em>−1 = (<em>x</em><em>i</em>−1<em>,y</em><em>i</em>−1)</li>

  </ul></li>

</ul>

I <em>p<sub>i </sub></em>= (<em>x<sub>i</sub>,y<sub>i</sub></em>)

I represents change in location from time <em>i </em>− 1 to time <em>i</em>

<ul>

 <li>Example:</li>

</ul>

<em>m</em><sub>1 </sub>= ((4<em>,</em>5)<em>, </em>(5<em>,</em>6)) <em>m</em><sub>2 </sub>= ((5<em>,</em>6)<em>, </em>(5<em>,</em>8)) <em>m</em><sub>3 </sub>= ((5<em>,</em>8)<em>, </em>(6<em>,</em>10)) <em>m</em><sub>4 </sub>= ((6<em>,</em>10)<em>, </em>(8<em>,</em>12))

<ul>

 <li><em>path</em>: list of locations [<em>p</em><sub>0</sub><em>,p</em><sub>1</sub><em>,p</em><sub>2</sub><em>,…,p<sub>n</sub></em>]

  <ul>

   <li>represents sequence of moves (<em>p</em><sub>0</sub><em>,p</em><sub>1</sub>)<em>, </em>(<em>p</em><sub>1</sub><em>,p</em><sub>2</sub>)<em>, </em>(<em>p</em><sub>2</sub><em>,p</em><sub>3</sub>)<em>, ,…, </em>(<em>p<sub>n</sub></em><sub>−1</sub><em>,p<sub>n</sub></em>) I Example: [(4<em>,</em>5)<em>, </em>(5<em>,</em>6)<em>, </em>(5<em>,</em>8)<em>, </em>(6<em>,</em>10)<em>, </em>(8<em>,</em>12)]</li>

  </ul></li>

 <li>If a move or path intersects a wall, it <em>crashes</em>, otherwise it is <em>safe</em></li>

</ul>

<h1>Objective</h1>

<ul>

 <li><em>Finish line</em>:

  <ul>

   <li>an edge <em>f </em>= ((<em>q,r</em>)<em>,</em>(<em>q</em><sup>0</sup><em>,r</em><sup>0</sup>))</li>

  </ul></li>

</ul>

I always horizontal or vertical

<ul>

 <li>Want to reach the finish line with as few moves as possible</li>

 <li>Find a path [<em>p</em><sub>0</sub><em>,p</em><sub>1</sub><em>,…,p<sub>n</sub></em>] I <em>p<sub>n </sub></em>must be on the finish line</li>

 <li>∃<em>t, </em>0 ≤ <em>t </em>≤ 1, such that <em>p<sub>n </sub></em>= <em>t</em>(<em>q,r</em>) + (1 − <em>t</em>)(<em>q</em><sup>0</sup><em>,r</em><sup>0</sup>)

  <ul>

   <li>Final velocity must be (0<em>,</em>0)</li>

  </ul></li>

 <li>Thus <em>p<sub>n</sub></em>−<sub>1 </sub>= <em>p<sub>n</sub></em></li>

</ul>

Example:      [(4<em>,</em>5)<em>, </em>(5<em>,</em>6)<em>, </em>(5<em>,</em>8)<em>, </em>(6<em>,</em>10)<em>, </em>(8<em>,</em>12)<em>, </em>(11<em>,</em>13)<em>, </em>(15<em>,</em>13)<em>,</em>

(19<em>,</em>12)<em>, </em>(22<em>,</em>11)<em>, </em>(24<em>,</em>10)<em>, </em>(25<em>,</em>9)<em>, </em>(25<em>,</em>8)<em>, </em>(25<em>,</em>8)]




<h1>Things I’ll provide</h1>

I’ll post a zip archive that includes the following:

I fsearch.py – domain-independent forward search algorithm

<ul>

 <li>can do depth first, best first, uniform cost, A*, and GBFS</li>

 <li>has hooks for calling a drawing package to draw search spaces I py – code to draw search spaces for racetrack problems</li>

</ul>

I racetrack.py – code to run fsearch.py on racetrack problems

I sample probs.py – Some racetrack problems I created by hand

I make random probs.py – Code to generate random racetrack problems

<ul>

 <li>not very good; we probably won’t use it</li>

</ul>

I sample heuristics.py – Some heuristic functions for Racetrack problems

I nmoves.py – An admissible heuristic function for Racetrack problems

I run tests.bash – a customizable shell script to run experiments

<ul>

 <li>you <em>must </em>customize it in order to use it</li>

</ul>

Here are some details <em>…</em>

<h1>fsearch.py</h1>

Domain-independent forward-search algorithm

I Implementation of Graph-Search-Redo

<ul>

 <li>main(s0,next states,goal test,strategy, h=None,verbose=2,draw edges=None) I s0 – initial state</li>

</ul>

I next states(<em>s</em>) – function that returns the possible next states after <em>s</em>

I goal test(<em>s</em>) – function that returns True if <em>s </em>is a goal state, else False

<sup>I </sup>strategy – one of ‘bf’, ‘df’, ‘uc’, ‘gbf’, ‘a*’

I h(<em>s</em>) – heuristic function, should return an estimate of <em>h</em><sup>∗</sup>(<em>s</em>)

<sup>I </sup>verbose – one of 0, 1, 2, 3, 4

<ul>

 <li>how much information to print out (see documentation in the file)</li>

</ul>

I draw edges – function to draw edges in the search space

<h1>racetrack.py</h1>

Code to run fsearch.main on racetrack problems

<ul>

 <li>main(problem,strategy,h,verbose=0,draw=0,title=”)</li>

</ul>

<sup>I </sup>problem – [s0, finish line, walls]

<sup>I </sup>strategy – one of ‘bf’, ‘df’, ‘uc’, ‘gbf’, ‘a*’

I h(<em>s,f,w</em>) – heuristic function for racetrack problems

<ul>

 <li><em>s </em>= state, <em>f </em>= finish line, <em>w </em>= list of walls</li>

 <li>py converts this to the <em>h</em>(<em>s</em>) function that fsearch.main needs</li>

</ul>

<sup>I </sup>verbose – one of 0, 1, 2, 3, 4 (same as for fsearch.py)

I draw – either 0 (draw nothing) or 1 (draw problems, node expansions, solutions)

I title – a title to use at the top of the graphics window

<ul>

 <li>default is the names of the strategy and heuristic</li>

 <li>Some subroutines that may be useful <em>…</em></li>

</ul>




<ul>

 <li>intersect(e1,e2) returns True if edges e1 and e2 intersect, False otherwise</li>

</ul>

<table width="623">

 <tbody>

  <tr>

   <td width="479">intersect([(0,0),(1,1)], [(0,1),(1,0)])</td>

   <td width="84">returns</td>

   <td width="59">True</td>

  </tr>

  <tr>

   <td width="479">intersect([(0,0),(0,1)], [(1,0),(1,1)])</td>

   <td width="84">returns</td>

   <td width="59">False</td>

  </tr>

  <tr>

   <td width="479">intersect([(0,0),(2,0)], [(0,0),(0,5)])</td>

   <td width="84">returns</td>

   <td width="59">True</td>

  </tr>

  <tr>

   <td width="479">intersect([(1,1),(6,6)], [(5,5),(8,8)])</td>

   <td width="84">returns</td>

   <td width="59">True</td>

  </tr>

  <tr>

   <td width="479">intersect([(1,1),(5,5)], [(6,6),(8,8)])</td>

   <td width="84">returns</td>

   <td width="59">False</td>

  </tr>

 </tbody>

</table>

Basic idea (except for some special cases)

I Suppose e1), e2

I Calculate the lines that contain the edges

<ul>

 <li><em>y </em>= <em>m</em><sub>1</sub><em>x </em>+ <em>b</em><sub>1</sub>; <em>y </em>= <em>m</em><sub>2</sub><em>x </em>+ <em>b</em><sub>2</sub></li>

</ul>

I If <em>m</em><sub>1 </sub>= <em>m</em><sub>2 </sub>and <em>b</em><sub>1 </sub>6= <em>b</em><sub>2 </sub>then parallel, don’t intersect

I If <em>m</em><sub>1 </sub>= <em>m</em><sub>2 </sub>and <em>b</em><sub>1 </sub>= <em>b</em><sub>2 </sub>then collinear ⇒ check for overlap

<ul>

 <li>Does either edge have an endpoint that’s inside the other edge?</li>

</ul>

I If <em>m</em><sub>1 </sub>6= <em>m</em><sub>2 </sub>then calculate the intersection point <em>p</em>

<ul>

 <li>The edges intersect if they both contain <em>p</em></li>

 <li>crash(e,walls)</li>

 <li>e is an edge</li>

 <li>walls is a list of walls</li>

</ul>

I True if e intersects at least one wall in walls, else False

<ul>

 <li>Example:</li>

</ul>

crash([(8,12),(10,13)],walls) returns False crash([(8,12),(9,14)],walls) returns True

<ul>

 <li>children(state,walls)

  <ul>

   <li>state, list of walls</li>

  </ul></li>

</ul>

I Returns a list [<em>s</em><sub>1</sub><em>,s</em><sub>2</sub><em>,…,s<sub>n</sub></em>]

<ul>

 <li>each <em>s<sub>i </sub></em>is a state that we can move to from state without crashing</li>

 <li>Example:

  <ul>

   <li>current state is ((8<em>,</em>12)<em>,</em>(2<em>,</em>2))</li>

  </ul></li>

</ul>

I 9 possible states, 5 of them crash into the obstacle

<sup>I </sup>children(((8,12),(2,2)), walls) returns

[((9,13),(1,1)), ((10,13),(2,1)), ((11,13),(3,1), ((11,14),(3,2))]




<h1>tdraw.py</h1>

<ul>

 <li>py draws search search graphs using Python’s turtle graphics I You won’t interact with turtle graphics directly</li>

 <li>In most cases it should run with no problem</li>

 <li>If it doesn’t:</li>

</ul>

I Do your computer and your Python installation have Tk support?

I If not, probably you can install Tk on your computer and re-install Python

I If that doesn’t work, you can run racetrack.main with draw = 0

<h1>sample heuristics.py</h1>

Three heuristic functions for the Racetrack domain:

<ul>

 <li>h edist(<em>s,f,walls</em>) returns Euclidean distance from <em>s </em>to the goal, ignoring walls</li>

</ul>

I Not admissible, but finds near-optimal solutions

I Problems

<ul>

 <li>can go in the wrong direction because it ignores walls</li>

 <li>can overshoot because it ignores the number of moves needed to stop</li>

 <li>h esdist(<em>s,f,walls</em>) is a modified version of h edist I includes an estimate of how many moves it will take to stop</li>

 <li>avoids overshooting</li>

</ul>

I still can go in the wrong direction because it ignores walls

sample heuristics.py (continued)

<ul>

 <li>h walldist(<em>s,f,walls</em>):</li>

</ul>

I The first time it’s called:

<ul>

 <li>For each gridpoint that’s not inside a wall, cache a rough estimate of the distance to the finish line</li>

 <li>Breadth-first search backwards from the finish line, one gridpoint at a time</li>

</ul>

I On all subsequent calls

<ul>

 <li>Retrieve the cached value</li>

 <li>Add an estimate of how many moves needed to stop</li>

</ul>

<h1>nmoves.py</h1>

Another heuristic function:

<ul>

 <li>h nmoves(<em>s,f,walls</em>):</li>

</ul>

I Calculates how many moves would be needed to reach the finish line if there were no walls

I It’s admissible, but I don’t recommend using it

<ul>

 <li>A* finds optimal solutions (vs. near-optimal with h esdist), but does about 10 times as many node expansions</li>

 <li>With h esdist, GBFS expands about the same number of nodes, and h esdist has lower overhead</li>

</ul>

– simple calculations vs. a recursive computation

<ul>

 <li>Like h esdist, h nmoves ignores walls, so can go in the wrong direction</li>

</ul>

<h1>What to do</h1>

<ul>

 <li>Write a better heuristic function than h walldist

  <ul>

   <li><em>Don’t </em>just make minor modifications to h walldist, you need to write something of your own</li>

  </ul></li>

 <li>Look for something that works just as well, but runs faster I Avoid caching distances for <em>all </em>the gridpoints I Some of them don’t matter; others don’t matter <em>much </em>I How to tell which ones?</li>

 <li>Experiment to see what works best</li>

 <li>Another possibility might be to try improving the heuristic estimates so that A* expands fewer nodes or GBFS finds shorter solutions

  <ul>

   <li><em>Warning</em>: I don’t advise doing this one</li>

  </ul></li>

</ul>

I I doubt you’ll be able to get significant improvements


