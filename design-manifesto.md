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
- memory allocator utility classes, for various allocation schemes
- efficient frame rate and a capable rendering module, with useful types
- a decent audio module - need to gain some experience working with sounds in general
- sensible input gathering, including rising/falling keypress status detection
- a reasonable separation of engine and content, so that different games entirely, or different versions of the same
game (including mods), can be built using the engine without too much difficulty

The target game is a Minecraft clone with a focus on higher granularity (the block size is half that of MC along each edge, or an eighth by volume) 
and dynamic world elements


## Language and Style

I will be using C++, since it is an industry standard language. I have some familiarity with the language, since it is what I taught myself when I first
started programming. At the time I hardly knew what I was doing. Now I have nearly completed a computer science degree and I am in love with C (and I tolerate Java), and I want to revisit C++. As things currently stand, I think of programs in a C-style, and I like the level of modular organization it presents, but I
wish it had some features that C++ does like templates. I am not entirely comfortable with the immense amount of features in the C++ standard library, nor with
a strictly object-oriented design mindset; but I am willing to dip my toes into the water, so to speak.

I will use a few stylistic guidelines/conventions that I think make sense:

1. Use little to no inheritance, at least in the engine components.
2. Function names will generally start with capital letters
3. Class names will generally start with capital letters; methods with lowercase; and member variables with the `m_` prefix
4. The program will be organized into logical modules (NOT the C++20 modules feature) through bulk header files - more on this below
6. Prefer using an explicit `Create_X()` function when calling into any module to create an object - that module will handle the allocation/construction itself, and return a relevant handle (pointer, index, whatever) to the given object
7. As much as possible, avoid using `new` and `delete` except at module initialization - pre-load OS memory allocations to the engine startup, giving large blocks of memory to custom allocators for each module
8. While the engine runs, allocate on the fly using custom allocators for speed and efficiency as needed

In general, as I am more used to C, I will follow a more C-oriented style, while trying to take advantage of and learn some C++ features.
What are logically 'modules' in the engine will correspond to namespaces with their externally visible functions and types declared in a single header file, and internal workings implemented across several individual `.cpp` files. 
This is to make the modularity clear, and to make the number of places I have to edit things upon making changes minimal. 

For example, the `Render` module might consist of:
- A single `Render.h` header, defining functions like `Render::Init()` and `Render::Draw()` and types like `Render::Mesh` and `Render::Texture`
- Individual `.cpp` files for each type, e.g. `Mesh.cpp` and `Texture.cpp`, defining functions like `Create_Mesh()` and `Load_Texture()`

## Design Documentation

Before writing code I will have an outline of the logical goals and organizational structure it should have, including even UML diagrams where I find them useful. In particular I will try to have a good idea about the structure of each module and include design documents in this repo before I begin actually implementing it. I have a tendency to get excited about optimization, but I will try my best to only pre-optimize in cases where I know it will make a major difference, and otherwise only optimize based on observed, profiled issues. I will focus on the necessary groupings of data and behavior for each class, and how other parts of the 
engine, both internal and external to the module, should be able to interact with it.

