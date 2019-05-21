## About

We are currently taking the course Computer Graphics and Interaction
at KTH.  Creating a computer graphics related project is one of the
main goals of the course. This blog will follow our progress in that
project. The members of the project group are Gustav Nelson Schneider,
Timmy Nielsen and Joakim Lilja.

## Engine Design

Before starting on the actual particle system implementation, we
have spent quite a lot of time on designing and building the (non
manditory) engine. The structure of the engine is now pretty much
finished, although there are some parts which need minor cleanup as
well as some features left to implement, such as a camera system etc.
Our main goal when creating the engine was to make it easy to extend,
which we believe we have accomplished, meaning that adding the rest
of the features should prove to be quite easy.

The engine is designed around the idea of entity component systems.
This gives us many advantages compared to a more object oriented
approach. The pattern is used by many modern game engines, one notable
example being Unity. Having some prior experience in 3D-engine programming,
Gustav brought forth the idea of splitting functionality from data as
a good design decision for multiple reasons. The most significant reason
is the fact that there might be multiple systems of the engine which depend
on the same data. Another reason is that it becomes easier to
extend the engine with more functionality as the project grows.

The complexity of the codebase is one reason you might adopt this
pattern, another advantage is that we can keep related data close
together. This can make a huge impact on performance due to cache
locality. Designing the program to be easy on the cache is known
as Data Oriented Design (DOD). We don't really need such a complex
engine for the project we're planning, but it is nice to have one in
case we want to add some bling-bling to the demo. Creating a basic
entity component system isn't much more diffucult than a more traditional
object oriented approach. For a small project it probably adds some
complexity, but as the project grows we are convinced the complexity
will be reduced.

We provide a brief overview of the engine design below.
There are a lot of in-depth information on the pattern available on
the interwebs for the interested reader. If you want more details
about our specific implemation, the code is available in our github
repository. The engine design isn't the most relevant part of the
project as it is not mandatory. On the otherhand, considering we
have a blog to write, we might as well explain the whole process.

## Setup and initial project specification

We decided early on that we wanted to do a project related to 
rendering. After some discussion, we managed to narrow it down to either
realistic water rendering or similar GPU particle systems. We have not yet
started working on the project specifics, but at the moment it's
leaning towards creating a GPU particle system.

### Setup

Since our group consists of both Windows and Linux users, we first wanted
to create a project which is possible to build in both environments.
Gustav is the only member of the group who prefer working in Linux,
and as he has the most experience with build systems he gladly
took on creating a skeleton project which we could use as a starting point.
We needed a build system that was easy to use for Windows users as well as
being compatible with Linux, making CMake a reasonable choice.

We decided to use OpenGL as DirectX isn't cross compatible and Vulkan
would be too complicated. Furthermore, OpenGL was the only API that we
had prior experience using. Next, we needed some cross platform libraries
for creating our OpenGL context and loading OpenGL symbols. The libraries
we eventually decided on was GLFW (for creating the context) and GLEW 
(for symbol loading). We also decided to use GLM for the mathematical
calculations. We will probably want to add some sliders and such to
change the parameters in the demo we plan on making - we therefore
also include ImGUI as an dependency, which is easy to use, and
will probably help us with everything we need in the future.

We have also made smart pointer wrappers for some
commonly used OpenGL objects. This might not be the most optimal
solution, but at least it gives us some form of memory management
(which to be honest probably isn't necessary for this project).

As of writing this, we will probably start working on the underlying
architecture of the engine. We will also try to make the underlying
structure of the engine general enough to be usable for other stuff
than just rendering particle systems. This is more of an intellectual 
challenge for us and a chance to test out ideas rather than an
actual necessity. Gustav is currently reworking the architecture of another
engine with the purpose of being used in 64k Intro, and hopefully we can
implement some of the ideas from this project into that. One reason
why we might want a more general purpose engine is to be able to
see how the particle system interacts with other 3D objects in a scene.
And if we need a 3D-engine we might as well try and do a decent job.
The code would also be more reusable if we want to include it in a 
future project.

### GPU particle systems

There are multiple ways we could create a particle system and we have
not really decided exactly what approach we will use at the
moment. One quite straight forward approach would be to use transform
feedback. Our first proof of concept will probably use this
approach. On the other hand, we could probably achieve the same thing
storing the data in some kind of textures or utilizing compute
shaders.
