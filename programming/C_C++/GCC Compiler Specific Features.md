## GCC Constructor-Destructor Attribute
`__attribute__` is a GCC specific syntax;not a function or a macro.
1. `__attribute__((constructor))` syntax : This particular GCC syntax, when used with a function, executes the same function at the startup of the program, i.e before `main()` function. It runs when a shared library is loaded.
2. `__attribute__((destructor))` syntax : This particular GCC syntax, when used with a function, executes the same function just before the program terminates through `_exit`, i.e after `main()` function. It runs when the shared library is unloaded

The way constructors and destructors work is that the shared object file contains special sections (`.ctors` and `.dtors` on ELF) which contain references to the functions marked with the constructor and destructor attributes, respectively. When the library is loaded/unloaded, the dynamic loader program checks whether such sections exist, and if so, calls the functions referenced therein.
```c
void __attribute__((constructor)) my_constructor_function(void) {
    // Initialization code executed before main()
}
```
Additionally, priority levels can be assigned to constructor functions using an integer value inside the double parentheses, ensuring a specific order of execution when multiple constructor functions are present:
```c
void __attribute__((constructor(10))) high_priority(void);
void __attribute__((constructor(9))) low_priority(void);
```