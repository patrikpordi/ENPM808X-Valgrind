# Valgrind Exercise

## Standard install via command-line
```bash
# Configure the project and generate a native build system:
  # Must re-run this command whenever any CMakeLists.txt file has been changed.
  cmake -S ./ -B build/
# Compile and build the project:
  # rebuild only files that are modified since the last build
  cmake --build build/
  # or rebuild everything from scracth
  cmake --build build/ --clean-first
  # to see verbose output, do:
  cmake --build build/ --verbose
# Run program:
  ./build/app/shell-app
# Clean
  cmake --build build/ --target clean
# Clean and start over:
  rm -rf build/
```

## Valgrind:
valgrind --leak-check=full --track-origins=yes ./build/app/shell-app > <OUTPUT_file-txt> 2>&1 

## Bugs:
- Unitialized variable in main.
- Memory had to be deallocated for the pointer.
## Outputs:
- out__commented.txt
- out_modifiedcode_commented.txt
- out_not_commented.txt
## Answers for extra credit:

- What happens when the executable is linked statically?
    It tries to compile everything in one single executable.
- Does Valgrind still detect those same bugs?
    If the executable is linked statically, Valgrind detects a broader range of memory-related errors, potentially resulting in false negatives, where actual issues are overlooked. 
- Why not?
    This is because numerous libraries in the shell-app and the CMake build of the project are dynamic. When you link libraries statically, their memory management behavior becomes integrated into your program's build, such as with CMake in this project. Valgrind may not distinguish between memory allocated by your program and that allocated by these libraries.

