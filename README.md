# naive-modules-ninja-generator
Toy and naive generator of ninja buildfiles for C++ modular projects

It can create ninja scripts for header-based projects (`--headers`) or for module-based projects (`--modules`).

If `--all-artifacts` is passed, `.o` and `.pcm` files would be built for all modules. If not (by default), only `.pcm`s would be built for modules with incoming dependencies, only `.o`s otherwise
(this tries to emulate a build where a lot of intermediate modules are used to build a few of binary artifacts).

Usage example:
```
python3 naive-generator.py --headers /path/to/h-and-cpps --modules /path/to/modules --compiler /path/to/clang [--all-artifacts]
```

The file `build.ninja` is written to the passed source directory.

Note that it does very simple module dependency scanning and assumes modules should be searched by name in the current directory.

All produced files are saved to the original directory, `ninja -t clean` should work as expected.

Assumptions:
  - All files are named *.cpp or *.h and are placed in the working directory
  - Module names match header names
  - clang with modules-ts support is used
  - Module dependency scanning is performing by looking at `import <name>;` declarations
  - in `--modules` mode, it assumes all cpps are module units
  
