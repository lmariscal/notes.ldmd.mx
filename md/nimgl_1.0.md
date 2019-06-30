# NimGL 1.0

NimGL has been in development since March of 2018, it started as a side project
to create and test a graphics library for Nim. A huge inspiration for the
project as to which modules to create was [LWJGL](https://lwjgl.org/),
since then I have added some modules and more bindings depending on the need of
the projects being developed and user feedback.  
At the same time, I have been studying Computer Science in Game Programming
since 2017. Just recently I needed to propose an idea for a thesis project. A
lot of other interesting projects came to mind, but NimGL still has room to grow
and can be an interesting proposition.

So NimGL 1.0 came to be, a semi-restart on the way the project was thought about.
A GitHub group was [created](https://github.com/nimgl) and a new domain was
bought [https://nimgl.dev/](https://nimgl.dev/). A change that was requested was
that all the bindings should be available as submodules. So it will be
implemented in their own repo under the GitHub's group.  
New generators will be written for most of the existing bindings, together with
better documentation related to Nim and helper modules to properly adapt this
bindings to the core Nim experience.

## ImGui (with helper example)

ImGui requires to push and pop certain states to be able to push to them, such
as windows, styles, fonts, and others. Using core Nim features such as templates
and macros certain functionality like RAII (stated in
[this ImGui's issue](https://github.com/ocornut/imgui/issues/2096)) and less
explicit (when needed) function declarations can be made.

*Current:*
```nim
discard igBegin("MyWindow")
discard igDragFloat3("pos", pos.x.addr)
igText("fps: %f", io.framerate)
discard igCheckbox("wireframe", wireframe.addr)
igEnd()
```

*Helper*
```nim
igBegin("MyWindow"):
  igDragFloat3("pos", pos.x.addr)
  igText("fps: %f", io.framerate)
  igCheckbox("wireframe", wireframe.addr)
```

It may seem like a little change (and I provided a small example), but after
hundreds of calls to the ImGui library this really starts to add.

## OpenGL

The current generator works fine, the issues come down to editing the
generator. This generator was made in under 2hrs, mostly because I needed some
modern OpenGL bindings for a school project. As a result, it lacks all the good
standards of code that you might think of. It will be rewritten and will have as
a new feature Extensions loadout. In the big scheme of things, I would love to
create a generator like [dav1d's](https://glad.dav1d.de/), but this will end up
being more like [glew](http://glew.sourceforge.net/). It is not a bad thing on
its own, but Extensions have to be loaded manually at runtime and before
loading the general library, which can be a turn off for some people since this
comes with bigger loading statements and OpenGL loader file.

## GLFW

I have been postponing the upgrade to version 3.3, mostly because it breaks
certain compatibility, and because GLFW was the first binding to be created so
it lacks a generator of any kind.  
It was my intention to integrate c2nim into this workflow, but it has failed in
several critical areas of generation. Creating a general-purpose translation
tool is a task of itself, but creating a single purpose unit that only works
with a certain header, and it works really well and to the lib's needs, can be
done. This will be applied to GLFW together with STB and will have their own
generators tailored to them.

## STB

Not really a lot to say, it lacks a lot of features that need to be implemented.
They will be implemented together with a generator of its own.

## Vulkan

Everything above sounds really nice, at least in my own perspective, both as the
developer and as an end user that would really appreciate these features. But it
doesn't add up to a thesis project if you also count in that most of the project
is already done and the new features are mostly what some people might call,
[syntatic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) or in general,
optimizations and improvements.

Vulkan is a rather new technology when you compare it with existing Graphics
APIs, that comes with a lack of educational resources and a lack of
frameworks, libraries and all that is needed to properly work with it. As such
a new Vulkan module will be added to the NimGL's collection (Vulkan Joins the
Battle!). This is still in the research stages and I still have to look at other
loaders and how they are implemented to avoid the same mistakes and to better
port it to Nim.

## Other

LWJGL binds a lot of other nice APIs'/libraries such as OpenAL, shaderc, OpenVR
and even Opus. I would love to add these modules to NimGL but they require
extensive knowledge of their usage and research on existing ports and even usage
of those ports to identify issues and how they would properly be ported to Nim.
Because of these reasons, they will be kept as an ideal state, but they will be
postponed until all the previously mentioned changes have been applied.

These changes and upgrades compose what will be called NimGL 1.0, the current
version will be kept bug free, and all the issues that are created will still be
addressed. I highly recommend that you properly tag NimGL's version or one of
its submodules in your Nimble file. All new development regarding version 1.0
will be kept on its own branch based on NimGL 0.3.6. Please notice that a lot
of syntax and integrations will break since I won't take into account
compatibility with existing versions. To keep my bow of taking care of this
repo, after version 1.0 has been released a new branch called version 0 will be
created as a LTS version. Where all issues related to this version will
be fixed and new (though small) improvements will be implemented.

Please let me know your thoughts on these changes on Twitter where you can find
me as [@thelmariscal](https://twitter.com/thelmariscal) where I am open to new and
different ideas.
