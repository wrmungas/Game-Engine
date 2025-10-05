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
- a reasonable separation of engine and content, so that different games entirely, or different versions of the same
game (including mods), can be built using the engine without too much difficulty

I also have a target game in mind, a kind of Minecraft clone with twice the LOD and a more dynamic and responsive world/environment.
This will influence what new engine features will be required. 
As I develop the engine, and use it for other projects, I will also add other features.



## Language and Style

I will be using C++, since it is an industry standard language. I am not entirely familiar with it: I originally taught myself
some programming basics in C++, but gave up when I became confused and overwhelmed. Now I have nearly completed a degree in 
computer science and I have a strong foundation in C and Java, and I want to come back to tackle the beast that is C++.

I will use a few stylistic guidelines/conventions that I think make sense:

1. Use little to no inheritance, at least in the engine components.
2. Function names will generally start with capital letters
3. Class names will generally start with capital letters; methods with lowercase; and member variables with the `m_` prefix
4. Prefer using an explicit `Create_X()` function when calling into any module to create an object - that module will handle the allocation/construction itself, and return a relevant handle (pointer, index, whatever) to the given object
5. As much as possible, avoid using `new` and `delete` except at module initialization - pre-load OS allocations to startup, giving large blocks of memory to custom allocators
6. While the engine runs, allocate on the fly using custom allocators from these memory regions for speed and efficiency to the use case

In general, as I am more used to C, I will follow a more C-oriented style, while trying to take advantage of and learn some C++ features.
What are logially 'modules' in the engine will correspond to namespaces with a single header file for the externally visible functions/types, and several individual implementation files. 
This is to make the modularity clear, and to make the number of places I have to edit things upon making changes minimal. 

For example, the `Render` module might consist of:
- A single `Render.h` header, defining functions like `Render::Init()` and `Render::Draw()` and types like `Render::Mesh` and `Render::Texture`
- Individual `.cpp` files for each type, e.g. `Mesh.cpp` and `Texture.cpp`, defining functions like `Create_Mesh()` and `Load_Texture()`

## Design Documentation

For each engine module, I will create a UML diagram for that module and identify key behaviors and types that should belong in it. 
I have a tendency to get excited about optimization, but I will try my best to only pre-optimize in cases where I know it will make a major difference, and otherwise
only optimize based on observed, profiled issues. I will focus on the necessary groupings of data and behavior for each class, and how other parts of the 
engine, both internal and external to the module, should be able to interact with it.
