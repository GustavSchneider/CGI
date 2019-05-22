## About

We are currently taking the course Computer Graphics and Interaction
at KTH.  Creating a computer graphics related project is one of the
main goals of the course. This blog will follow our progress in that
project. The members of the project group are Gustav Nelson Schneider,
Timmy Nielsen and Joakim Lilja.

## Transform Feedback
We followed our initial idea that we mentioned in the previous blog
post about starting off with transform feedback. Transform feedback
lets us update the data in GPU memory directly on the GPU instead of
sending it back and forth between CPU and the GPU. Transform Feedback
makes this possible by letting us output data to a OpenGL buffer in
the vertex shader or the geometry shader stage. Sending memory from
the CPU to the GPU is really slow, sending millions of particles to
the GPU every frame would overflow our memory bus, keeping the data on
the GPU is therefore really important enable us to render a lot of
particles.

The Transform feedback functionality was not that hard to implement as
it sort of is a part of the rasterization pipeline. Although it
required quite a few steps to setup. We managed to implement the
transform feedback quite fast (a quite a few hours) without any major
struggles. Note that transform feedback only works if you have created
a buffer on the GPU memory and actually sent the data to that buffer
to let the transform feedback update the data.

![Transform Feedback](https://i.stack.imgur.com/aUXj6.png)

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
