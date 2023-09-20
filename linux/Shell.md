# The `_` environment variable  
The `_` variable in unix shell serves as a placeholder for the most recent argument used in the last executed command. It is a convenient way to reference the previous command's arguments without having to retype them.
For example, if we run,
```bash
echo "hello world"
echo $_
```
We will get
```
Hello World
```
If there are more than one arguments then it stores the last argument.
If no argument is passed then it stores the 0th arg i.e. the command that was passed.

# `env -i` clearing env vars temporarily
To clear the environment variables temporarily and run some command use the following command
```bash
env -i COMMAND ARGS
```
