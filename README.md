# Game-Engine
Repository for code and design documents related to my game engine development.

For a discussion of the engine's design rationale / methodology, including the 
goals of the engine, the organization of components, and the coding style conventions
see the design-manifesto.md file. I maintain this file as an introductory point for 
anyone else looking into the repository; that file will be half for anyone looking to
examine, use, critique, or contribute to the engine, and half for myself while 
creating it. 

This file WILL outline how to use/build the engine. I have not fully settled on this
yet, but my initial plan is that the engine and the actual game content will be 
separated, though tightly coupled. The engine will be built to one object, and the
content code will be built to another which links with the engine to create the 
executable for a given version of the game, including modded versions. 

This repository will only contain code for the current version of the engine, except
perhaps some barebones content code to test it with.
