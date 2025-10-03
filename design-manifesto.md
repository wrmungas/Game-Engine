# Engine Design Manifesto

This document provides a rationale for the design of this engine, and guidelines
for the design and coding process. This document is as much for me, the creator, 
to remain consistent during development as it is for anyone else viewing the 
engine to understand it more completely.

## Motivation and Goals

I have created this engine to serve as a project that will accomplish a number of 
goals, including:
- growing my skills in general software design and project management
- learning (relearning?) C++
- learning (relearning?) graphics programming
- gaining experience tackling interesting problems with significant constraints, especially in the field of game development
- creating a framework with which I can make fun and enjoyable games, as well other GUI-based projects
- demonstrating skills/experience to potential future employers

These are what I hope to accomplish with the engine as a _project_, and these serve as benefits for me. 
I have additional goals for the actual performance and features of the engine, including:
- memory allocator utility classes, for various styles of allocation schemes
- efficient frame rate and a capable rendering module, with useful types and primitives
- a decent audio module
- sensible input gathering
- a separation of engine and content, so that different games entirely, or different versions of the same
game (including), can be built with it without too much difficulty

## Language and Style
I will be using C++, since it is an industry standard language. I am not entirely familiar with it: I originally taught myself
some programming basics in C++, but gave up when I became confused and overwhelmed. Now I have nearly completed a degree in 
computer science and I have a strong foundation in C and Java, and I want to come back to tackle the beast that is C++.
