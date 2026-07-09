THEORY: WHY PYTHON IS USED

1. Readability and low syntactic overhead
   Python's syntax closely mirrors plain English and mathematical
   notation (e.g. "if x in list:" instead of verbose loops with
   brackets and semicolons). This lowers the barrier between "thinking
   about a problem" and "expressing it in code," which is why it's
   favored for teaching, prototyping, and research where iteration
   speed matters more than raw execution speed.

2. Interpreted, dynamically typed nature
   Python code runs through an interpreter (CPython by default) rather
   than requiring a separate compile step. Variables aren't bound to
   fixed types at declaration — a name can point to an int, then a
   string, then a list. This trades some runtime performance for
   flexibility and faster development cycles: you write, run, and fix
   in tight loops without waiting on a build process.

3. "Batteries included" philosophy
   Python ships with a large standard library (file I/O, networking,
   JSON, regex, etc.) so many tasks need no external dependencies at
   all. Beyond that, PyPI hosts hundreds of thousands of third-party
   packages, meaning almost any problem (web scraping, ML, GUI,
   scientific computing) already has a mature library rather than
   requiring code from scratch.

4. Why it dominates data science and ML specifically
   - numpy gives Python C-level performance for numerical operations
     by storing data in contiguous typed arrays rather than Python's
     default object-per-element lists.
   - Libraries like pandas, scikit-learn, TensorFlow, and PyTorch are
     written with C/C++/CUDA backends but expose a Python front end —
     so you get Python's ease of use without sacrificing the speed of
     lower-level languages for the heavy computation itself.
   - This "glue language" role — orchestrating fast compiled code from
     an easy-to-write layer — is central to why Python became the
     default choice for ML/data work rather than a slower pure-Python
     alternative.

5. Cross-platform and general-purpose
   The same Python script typically runs unmodified on Windows, macOS,
   and Linux, since CPython abstracts OS-level differences. It's also
   general-purpose: the same language handles web backends (Django,
   Flask), automation scripts, data pipelines, and desktop tools — so
   teams avoid context-switching between languages for different parts
   of a stack.

6. Large community and ecosystem effects
   Popularity is partly self-reinforcing: more users → more
   libraries, tutorials, and StackOverflow answers → lower friction for
   new users → more adoption. This network effect is a major reason
   Python remains dominant in fields like AI/ML even when
   theoretically faster languages exist for the same tasks.

7. Trade-off it accepts
   Python is slower than compiled languages (C, C++, Rust, Go) for
   raw CPU-bound loops, due to interpretation overhead and dynamic
   typing checks at runtime. It compensates by pushing performance-
   critical work down into compiled extensions (numpy, C extensions)
   while keeping the orchestration layer — the 90% of code that
   isn't the bottleneck — fast to write and easy to maintain.