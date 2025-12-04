<div align="center"><h2> Hi there 👋 I'm glad you're here :)</h2></div>

[https://raw.githubusercontent.com/HenryMahnke/HenryMahnke/main/CDPRTraceUMN3.mov](https://github.com/user-attachments/assets/c76b7e72-457e-4ab4-9216-ce0a7af705a4)

Welcome to my github!
Here is a cool video of the robot that I worked on over the summer, showing some UMN pride! 

I work on a lot of projects, but am super involved with research, which is primarily closed source(not for long though!).
My research is on Cable Driven Parallel Robots(CDPRs) - think skycam (nfl camera robots) but bigger, better, more accurate, and more awesome in every way... 
These robots are not yet very commercially viable except in very particular cases, but the promise is massive: relative spacecraft motion, construction, large scale 3d printing, material handling in warehouses, even elevators are (sort of) a CDPR the list goes on and on! To support these efforts I split my time in 2 camps: research, and software development. 

For research, see my conference paper from CableCon 2025: [https://link.springer.com/chapter/10.1007/978-3-031-94608-0_1 | link_to_paper]
And see what I'm working on now: [https://github.com/HenryMahnke/SummerResearchPoster] (paper is being written)

For software development, we are developing a software ecosystem we call SPARC - Software Package for Actuation Robots (driven by) Cables - (you have to squint to see the acronym...)

This software ecosystem is comprised of 3 major parts: 

SPARC-SIM


SPARC-RT


SPARC-ROS


SPARC-SIM:
SPARC-SIM is our flagship research and experimentation software package, right now it features: 
trajectory planning(with spline and line path planning and a plethora of motion profiling options - trapezoidal, S-curve) as well as min-snap trajectory planning (not split up by path vs motion, just one step! it's an optimization formulation :) - largely developed my me, with more recent motion planning modernization with the RUCKIG package done by other software members


Inverse kinematics: given the payload position how long are the cables?!? - Done by me!


Forward kinematics: given the lengths of the cables, where is the payload(really hard - like IK of serial manipulators, numerical methods, potentiall infinite solutions, accounting for SAG?!?!? OH MY - this is my research area) - Done by me!


Inverse Dynamics: What forces and moments (wrench) do we need to apply to the payload to generate some acceleration - Done by myself, and a grad student from my lab


Tension distribution: The process of allocating the tensions to the cables given the wrench (Normally solved as a LP, QP, or some numerical approximation of a QP that is closed form but doesn't guarantee a solution) - Done by me (one of my favorite topics, optimization!)


Forward dynamics: given tensions what is the wrench applied to the payload - Done by me!


Workspace analysis (in many flavors): Becuase the robot is fundamentally limited by the tensions that can be produced from the cables, what are all of the places in space that we can actually go given some acceleration- how can we compute this efficiently and to a really high degree of accuracy? We use a ray casting method called WireX developed by andreas Pott - [https://www.researchgate.net/profile/Andreas_Pott/publication/334164626_WireX_-_An_Open_Source_Initiative_Scientific_Software_for_Analysis_and_Design_of_Cable-driven_Parallel_Robots/links/5d1b2e88458515c11c099757/WireX-An-Open-Source-Initiative-Scientific-Software-for-Analysis-and-Design-of-Cable-driven-Parallel-Robots.pdf | Link] - Done by me, along with discrete based methods, circle based sampling vs tetrahedron (no icosohedron yet)

Containerized: The sim is containerized, we use docker. The main reason is that it would be easier to get everyone using the same python version, versions of packages, same operating system, and extend to use mojo. Mojo is a new language developed by Chris Lattner(swift creator, LLVM compiler toolchain creator (runs almost every modern language))
More about it in future update... 
fun side note - we are beginning to use mojo to speed up computations, and the whole thing is containerized with docker YIPEEE!!!


SPARC-RT: 
SPARC-RT is our real time software package, written entirely in C++, featuring a terminal user interface, soft real time constraints(running on windows, but pinning to a core, and spin waiting ~150ns amortized jitter, 2ms cycle time). It implements many of the same algorithms from the sim, but in C++ with an emphasis on computational feasibility. The library that we are using is rigtorp::SPSCQueue for lock free bounded queues.



Other projects:
The other main projects I'm working on is dabbling around in mojo, trying to replicate some common robotics software patterns and algorithms in it because I am waiting for the day when I don't need to write any more C++ (and anymore Python...). 


I am also working on a beautified major planner application. At the University of Minnesota, figuring out the classes you are going to take to graduate is such a pain. You get a single PDF of what the plan is, but it's overly rigid, overly abstract, and there is no online interface for combining and mixing and matching majors and minors, creating multiple plans, planning out what classes you want to take to minimize graduation time, fulfill all of you general education requirements, and take classes that you actually enjoy. This project seeks to change that. It uses a fast API backend written in python, with a front end in React with NextJs. It would have been my preference to use Svelte, but I am not a fan of their new runes syntax with Svelte 5. While it is very similar to React now, anecdotally it seems then I should just use React, as it is more developed, so it's an interesting project to learn React with, and has been interesting so far! In terms of the optimization, the plan is to use Mixed Integer Linear Programming for the optimization. While it's still being prototyped, it seems mostly promising, but interested to see the compute time once it expands to the full course catalog avaliable to take at the University of Minnesota. 
