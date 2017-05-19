Embedded System Design
======================

# Documentation
- Document what code does not how it does.
- i++; //increment index . For God's sake don't do this.
- Create system diagrams for both hardware and software.
- __Hardware:__
  - Start with power block, to sub systems,
  sensors, outputs etc. list out the peripheral and communication being used.
- __Software:__
  - Make three diagrams.
  - Architecture diagram(database, algos, state machines, buffer systems, etc.)
  - Hierarchy of control organization (Fancy way of saying flowchart)
  - Software layering view.
- Keep consistant style in code refer https://google.github.io/styleguide/cppguide.html
- add a logging subsystem with log levels.
- Add a version string to the code in form of A.B.C(A-Major Version, B-Minor Version, C- build indicator), set build number to increment automatically, and have it acc

```C
static tBoolean gLogOnPrivate;
```
The static keyword means different things in different places. For functions and variables outside functions, the keyword means “hide me so no one else can see” and limits scope. For variables within a function, the static keyword maintains the value between calls, acting as a global variable whose scope is only the function it is declared in.