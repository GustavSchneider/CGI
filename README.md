## About
We are curretly taking the course Computer Graphics and Interaction at KTH.
Creating a computer graphics related project is one of the main goals of the 
course. This blogg will follow our progress in that project. The members of the 
project group are Gustav Nelson Schneider, Timmy Nielsen and Joakim Lilja.

## Setup and initial project specification
We decided early on that we wanted to do a project that was rendering related.
We then narrowed possible project down to rendering realistic water and GPU particle
systems. We have not yet started working on the project specifics of the project,
but at the moment creating a GPU particle system probaly is what we will make.

### Setup
Out group consists of both Windows and Linux users and we wanted to create a project
which is possible to build in both environments. Well, I am the only member of the
group who prefer working in Linux and has the most experience with build systems so
I took on creating a skelleton project we can use as a starting point. We needed a 
build system that is easy to use for the Windows people and also is compatible with
Linux, CMake was therefore a reasanoble choise (although CMake is not perfect).

We decided to use OpenGL as DirectX isn't cross compatible and Vulkan would be to complicated.
Also no one in our group has any experience with any other APIs than OpenGL from beforehand.
We therefore needed cross platform libraries
for creating our OpenGL context and loading OpenGL symbols. The libraries we decided to
use was GLFW for creating the context and GLEW for symbol loading. We also decided to use 
GLM for math stuff. We probably want to add some sliders and stuff to change some parameters 
in the demo we plan on making. I therefore included ImGUI as an dependency, which is easy
to include and use, and will probably do everything we need in the future.

I have also made some smart pointer wrappers for common some comonly used OpenGL objects.
This might not be the most optimal solution, but atleast gives us some kind of memory 
managment (which to be honset probably isn't necessary for this project).  

As of writing I will probably start working on the underlying architecture of the engine.
I will also try to make the undelying structure of the engine general enough to be used for o
ther stuff than just rendering particle systems. This is not realy needed but more of an 
intelectuall challange for me and a chance to test out ideas. I am currectly reworking
the architecture of another enigne with the purpose of being used in 64k Intro, so 
hopfully I can implement some of the ideas from this project into that.
One reason why we might want a more general engine would be that it might be good idea
to see how the particle system interacts with other 3D object in a scene. And if we
need a 3D-engine we might aswell do a decent job at it. The code would also be more
reusable if we want to include it in another project in the future.

### GPU particle systems
There is multiple ways we could create a particle system and we have not realy decided
exactly what approach we will use at the moment. One quite straight forward approach
would be to use transform feedback. Our first proof of concept will probably use this
approach. On the other hand we could probably achieve the same thing storing the data
in some kind of textures or utilizing compute shaders.
