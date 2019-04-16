## About

We are currently taking the course Computer Graphics and Interaction
at KTH.  Creating a computer graphics related project is one of the
main goals of the course. This blog will follow our progress in that
project. The members of the project group are Gustav Nelson Schneider,
Timmy Nielsen and Joakim Lilja.

## Engine Design

While waiting on the particle system part of the project to begin. I
have been working alot on the (non manditory) engine. The structure of
the engine is pretty much finished. There is some parts which need
some minor cleanup and some features such as camera system left to
implement.  My main goal with the engine was to make extending it
easy, which I think I have accomplished, so adding the lacking
features should be quite easy.

The engine is designed around the idea of entity component systems.
This gives us many advantages over a more object oriented
approach. The pattern is used by many modern game engines, one notable
example is Unity. I've written a few 3D-engines in the past, after a
while you realize that splitting functionality from the data is a good
design decision for multiple reasons. One major reason is that there
might be multiple systems of the engine which are dependant on the
same data. Using the pattern also makes it easier to extend the engine
with more functionality when the project grows.

The complexity of the codebase is one reason you might adopt the
pattern, another advantage is that we can keep related data close
together, this can make a huge impact on performance due to cache
locality. Designing the program to be nice on the cache is usally
called Data Oriented Design (DOD). We don't really need such complex
engine for the project we plan on doing, but it is nice to have one if
we want to add some bling-bling to the demo. Creating a basic entity
component system isn't much more diffucult than a more traditional
object oriented approach. For a small project it probably adds some
complexity, but when the project grows I am certain the complexity
will be reduced using such sytem.

We wont give more than a very brief overview on the engine
design. There are a lot of texts on the interwebs which describes the
pattern in more depth. If you want more information about the
implemation details, you can find the code in the github
repository. The engine design isn't the most relevant part of the
project and to be fair not even necessary. On the otherhand, now when
we have this blog we might explain the whole process.

## Setup and initial project specification

We decided early on that we wanted to do a project that was rendering
related.  We then narrowed possible project down to rendering
realistic water and GPU particle systems. We have not yet started
working on the project specifics of the project, but at the moment
creating a GPU particle system probably is what we will make.

### Setup

Out group consists of both Windows and Linux users and we wanted to
create a project which is possible to build in both
environments. Well, I am the only member of the group who prefer
working in Linux and has the most experience with build systems so I
took on creating a skeleton project we can use as a starting point. We
needed a build system that is easy to use for the Windows people and
also is compatible with Linux, CMake was therefore a reasonable choise
(although CMake is not perfect).

We decided to use OpenGL as DirectX isn't cross compatible and Vulkan
would be to complicated.  Also no one in our group has any experience
with any other APIs than OpenGL from beforehand.  We therefore needed
cross platform libraries for creating our OpenGL context and loading
OpenGL symbols. The libraries we decided to use was GLFW for creating
the context and GLEW for symbol loading. We also decided to use GLM
for math stuff. We probably want to add some sliders and stuff to
change some parameters in the demo we plan on making. I therefore
included ImGUI as an dependency, which is easy to include and use, and
will probably do everything we need in the future.

I have also made some smart pointer wrappers for common some commonly
used OpenGL objects.  This might not be the most optimal solution, but
at least gives us some kind of memory management (which to be honest
probably isn't necessary for this project).

As of writing I will probably start working on the underlying
architecture of the engine.  I will also try to make the underlying
structure of the engine general enough to be used for other stuff
than just rendering particle systems. This is not really needed but
more of an intellectual challenge for me and a chance to test out
ideas. I am currently reworking the architecture of another engine
with the purpose of being used in 64k Intro, so hopefully I can
implement some of the ideas from this project into that.  One reason
why we might want a more general engine would be that it might be good
idea to see how the particle system interacts with other 3D object in
a scene. And if we need a 3D-engine we might aswell do a decent job at
it. The code would also be more reusable if we want to include it in
another project in the future.

### GPU particle systems

There is multiple ways we could create a particle system and we have
not really decided exactly what approach we will use at the
moment. One quite straight forward approach would be to use transform
feedback. Our first proof of concept will probably use this
approach. On the other hand we could probably achieve the same thing
storing the data in some kind of textures or utilizing compute
shaders.
