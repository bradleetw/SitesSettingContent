---
title: Julia
menu:
  sidebar:
weight: -255
slug: Julia
---

Julia 語言的官網: https://julialang.org/

Julia 在 Github: https://github.com/JuliaLang

Julia 學習資源: https://lectures.quantecon.org/jl/index_learning_julia.html

Julia 學習資源2: http://ucidatascienceinitiative.github.io/IntroToJulia/

Julia machine learning 學習資源: ~/Projects/julia_study/MLCrashCourse

Julia's tours: http://www.numerical-tours.com/julia/


### REPL (Read Eval Print Loop)
REPL 也就是 Juila interpreter.

some basic command:

1. type `?` -> change to `help?>`, access to online documentation.

2. type `;` -> get a shell prompt, `shell>`, at which you can enter shell commands.

3. type `]` -> enter package management mode, `(v1.0) pkg>`, you could add/update/remove package in this mode.

#### Package REPL-mode.
Type `]` key first to enter package REPL-mode:

1. Press backspace when the input line is empty, or press Ctrl+C to return the `julia>` prompt.

2. `(v1.0) pkg> status` or `(v1.0) pkg> st`, showing the list of installed packages.

3. `(v1.0) pkg> add packageName`, adding a new package to project.

4. `(v1.0) pkg> update` or `(v1.0) pkg> up`, updating packages in mainfest.

5. `(v1.0) pkg> remove packageName` or `(v1.0) pkg> rm packageName`, removing packages from project or manifest.

You also could manage package under `julia>` prompt.

1. `julia> using Pkg`: loading `Pkg` module. `julia> import Pkg`?


2. `julia> Pkg.status()`

3. `julia> Pkg.add("packageName")`

4. `julia> Pkg.update()`

5. `julia> instantiate` ?

6. `julia> activate someProjectName`? like python virtual env

7. `julia> precompile`


---
