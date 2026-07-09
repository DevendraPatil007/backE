THEORY: HOW PYTHON PACKAGE INSTALLATION WORKS

1. What pip actually does
   pip (Pip Installs Packages) is Python's package manager. When you run
   "pip install numpy pandas", it:
   a) Contacts PyPI (Python Package Index, pypi.org) — the central repository
      hosting Python packages
   b) Resolves dependencies — pandas requires numpy, python-dateutil, and
      pytz, so pip builds a dependency graph and figures out compatible
      versions of everything
   c) Downloads "wheels" (.whl files) — prebuilt binary packages matching
      your OS, Python version, and CPU architecture (e.g.
      numpy-1.26.4-cp311-cp311-manylinux_x86_64.whl). This avoids compiling
      C/Fortran code from source, which numpy and pandas are largely
      written in for performance.
   d) If no matching wheel exists for your platform, pip falls back to
      downloading the source distribution (.tar.gz) and compiling it
      locally, which requires a C compiler and can take much longer.
   e) Installs everything into site-packages, the directory Python scans
      for importable modules.

2. Why numpy and pandas specifically
   - numpy provides the ndarray, a fixed-type, contiguous memory block
     implemented in C. This is what makes numerical operations fast
     compared to native Python lists (which store pointers to scattered
     PyObjects).
   - pandas is built on top of numpy. Its DataFrame is essentially a
     collection of numpy arrays (one per column, historically via
     "blocks") with labeled indexing, missing-data handling, and I/O
     tools layered on top.
   - This is why pandas installation always pulls numpy in as a
     dependency — it's not optional infrastructure, it's the underlying
     data structure.

3. Why environments matter (the theory behind venv)
   - Every Python interpreter has one associated site-packages directory
     by default. If you have multiple projects needing different
     versions of pandas (e.g. one needs pandas 1.5 for legacy code,
     another needs 2.x), installing globally causes version collisions.
   - A virtual environment (venv) is a lightweight copy of the Python
     interpreter with its own isolated site-packages. Activating it
     rewires your shell's PATH so "python" and "pip" point to the venv's
     binaries instead of the system ones.
   - This is why python3 -m venv creates a "venv" folder containing
     bin/, lib/, and pyvenv.cfg — it's a self-contained sandbox, not a
     separate Python install.

4. Why "externally-managed-environment" errors happen
   - Debian/Ubuntu (since ~23.04) and Homebrew Python began marking the
     system Python as "externally managed" (PEP 668). The OS itself
     relies on certain Python packages for system tools, so it blocks
     pip from freely modifying that same environment to prevent
     breaking the OS.
   - Virtual environments, --user installs, or pipx are the sanctioned
     workarounds because they don't touch the system-managed
     site-packages.

5. conda as an alternative theory
   - conda is not just a Python package manager — it manages binary
     dependencies at the OS level too (including non-Python libraries
     like BLAS/LAPACK, which numpy relies on for fast linear algebra).
   - This is why conda installs of numpy/pandas can sometimes be faster
     or more stable on certain platforms — it ships optimized, precompiled
     binary libraries (like Intel MKL) rather than relying on whatever
     the wheel bundles.