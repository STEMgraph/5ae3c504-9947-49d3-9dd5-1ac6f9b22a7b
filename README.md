<!---
{
  "id": "5ae3c504-9947-49d3-9dd5-1ac6f9b22a7b",
  "teaches": "Introduction to GNU Make",
  "depends_on": ["302c98a7-cbea-435c-ada2-bbf7538429a2"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-04",
  "keywords": ["compilation", "automation", "toolchain"]
}
--->

## Introduction

`make` is a build automation tool originally created by Stuart Feldman in 1976. It was designed to automatically determine which pieces of a large program need to be recompiled and to issue the commands to recompile them. `GNU make` is the most widely used version today.

This exercise introduces the concept of *Makefiles*, shows how to automate compilation of simple C programs, and builds the mental model of a *dependency graph* for code projects.

Understanding `make` lays a strong foundation for working with larger projects, understanding CI/CD pipelines, and using tools like `CMake`.

## Tasks

1. **Hello Makefile**

    Write a `Makefile` for the following program:

    ```c
    // hello.c
    #include <stdio.h>

    int main() {
        printf("Hello, Make!\n");
        return 0;
    }
    ```

    Your Makefile should:
    - Compile `hello.c` to an executable called `hello`
    - Include a `clean` target to remove the executable

2. **Add Dependencies**

    Now split your code into two files:

    ```c
    // main.c
    #include "greeter.h"

    int main() {
        greet();
        return 0;
    }

    // greeter.c
    #include <stdio.h>
    #include "greeter.h"

    void greet() {
        printf("Hello from greeter.c\n");
    }

    // greeter.h
    void greet();
    ```

    Update the `Makefile` to compile this multi-file program.

3. **Automatic Variables and Pattern Rules**

    Refactor your `Makefile` to use automatic variables like `$@`, `$<`, and `$^`. Use pattern rules like:

    ```make
    %.o: %.c
        $(CC) -c $< -o $@
    ```

4. **Add a Debug Target**

    Add a `debug` target to compile with the `-g` flag and no optimization.

5. **Phony Targets**

    Declare your non-file targets (`clean`, `debug`, etc.) as `.PHONY`.

## Questions

1. What is the purpose of a `Makefile` in a software project?
2. What happens if a `.c` file is modified but the corresponding `.o` file is not?
3. How does `make` decide which files to recompile?
4. What are `.PHONY` targets and why are they important?
5. Why might one use `make` instead of a shell script for compiling?

## Advice

- Use `make -n` to preview what commands would be run without executing them.
- Try intentionally breaking a dependency and running `make` again to observe its behavior.
- Study the output of `make -d` to understand its internal decision process.
- This is a great place to discuss how tools like `gcc`, `make`, and `ld` form the basis of a toolchain.
- If you're curious, explore how `ninja` and `CMake` relate to `make`.

> 💡 Stuart Feldman’s *make* was one of the first tools to formalize software build logic. For more, see his ACM talk: *“The Making of Make”*.
