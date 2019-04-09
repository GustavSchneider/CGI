## About
This project blog will follow our progress in our project in the course
Computer Graphics and Interaction at KTH. The members of the project are
Gustav Nelson Schneider, Timmy Nielsen and Joakim Lilja.

## Setup and initial project specification
We decided early on that we wanted to do a project that was rendering related.
We then narrowed possible project down to rendering realistic water and GPU particle
systems. We have not yet started working on the project specifics of the project,
but at the moment creating a GPU particle system probaly is what we will make.

### Setup (Gustav Nelson Schneider
Out group consists of both Windows and Linux users and we wanted to create a project
which is possible to build in both environments. Well, I am the only member of the
group who prefer working in Linux and has the most experience with build systems so
I took on creating a skelleton project we can use as a starting point. We needed a 
build system that is easy to use for the Windows people and also is compatible with
Windows, CMake was therefore a reasanoble choise (although CMake is not perfect).

We decided to make the project using OpenGL so we also needed a cross platform libraries
for creating our OpenGL context and loading OpenGL symbols. The libraries we decided to
use was GLFW, GLEW. We also decided to use GLM for math stuff. I also realized that we
probably want to add some sliders and stuff to change some parameters of the demo in
the future. I therefore included ImGUI as an dependency, which is easy to include and
use, and will probably do everything we need in the future.

I have also made some smart pointer wrappers for common some comonly used OpenGL objects.
This might not be the most optimal solution, but atleast gives us some kind of memory 
managment (which probably isn't necessary for this project).

### GPU particle systems
There is multiple ways we could create a particle system and we have not realy decided
exactly what approach we will use at the moment. One quite straight forward approach
would be to use transform feedback. We could proably achieve the same thing storing
all the data in some kind of texture or utilizing compute shaders. Our first proof of
concept will probably be using transform feedback.
