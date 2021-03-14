# E:C at Olin Research Paper

Paper: [Designing a small-footprint curriculum in computer science (Allen B. Downey and Lynn Andrea Stein)](https://greenteapress.com/thinkpython/swampy/downey-stein-fie.pdf)

This paper was written after only two full iterations of E:C curriculum were taught at Olin College.

The curriculum outline then:

###### Intro Courses
1. Introduction to Programming (defunct)
2. Software Design

###### Core Computing Courses
1. Foundations of Computer Science (Now can be swapped for Data Structures and Algorithms)
2. Software Systems (this class)

###### Other Courses/Electives
1. Discrete Math
2. Computer Architecture
3. Synchronization (defunct)
4. Computer Systems and Public Policy (defunct)
5. Human Factors and Interface Design (defunct)
6. Computational Modeling (defunct)

### Software Systems as envisioned by Allen and Lynn
- "compressing three semesters into one": networks, operating systems, database implementation
- start with two-parameter model of communication (transmission time as function of latency and bandwidth)
- bring connection between data structure design and file system design
  - database implementation is an example of a file system designed to support a particular set of instructions
- Experimental design
  - exercise-based learning
- Combining networks and operating systems in one class reflects tech trend towards distributed systems
- Readings of research papers
- No modifications at the kernel level
- Don't cover deadlock detection or recovery
- Synchronization covered briefly
- Limited to Linux work; don't see wide range of solutions
- Second half of semester is project-based
