# Important Functions
---
***All the functions are defined in `stdio.h`, unless stated otherwise.***
***EOF is a macro defined in `stdio.h` which holds the value `-1`.***
#### File Open Error Checking
```c
FILE *file = fopen("data.bin", "wb");
// always check File opening errors!!
if (file == NULL) {
    perror("Error opening file");
    return 1;
}
```
#### Flushing the Buffer
In order to improve efficiency, most file system implementations write data to disk one sector at a time. Therefore, data is buffered until a sector's worth of information has been output before the buffer is physically written to disk. When you call `fclose( )`, it automatically writes any information remaining in a partially full buffer to disk. This process is called ***flushing the buffer.***

---
### `FILE fopen("path", "mode")`

- **Returns**: On success, returns the address of the file; on failure, returns NULL.
- **Modes**:
  - `r`: Read (Open file for input operations. The file must exist.)
  - `w`: Write (Create an empty file for output operations.)
  - `a`: Append (Open file for output at the end of a file.)
  - `r+`: Read/Update (Open a file for both input and output.)
  - `w+`: Write/Update (Create an empty file for both input and output.)
  - `a+`: Append/Update (Open a file for both input and output with output operations at the end of the file.)
  - `r+b` or `rb+`: Open a binary file for read/write.
  - `w+b` or `wb+`: Create a binary file for read/write.
  - `a+b` or `ab+`: Append or create a binary file for read/write.

### `int fclose(FILE *stream)`

- **Returns**: 0 on success, EOF on failure.
- The `fclose()` function closes the file associated with `stream` and disassociates the stream from the file. It also flushes the buffer.
- Never call `fclose( )` with an invalid argument. Doing so will damage the file system and possibly cause irretrievable data loss.

### `size_t fread(void *ptr, size_t size, size_t count, FILE *stream)`

- **Returns**: The total number of elements successfully read. 
- Reads data from the file specified by `stream` into the memory pointed to by `ptr`.
- If the return value differs from the `count` parameter, it indicates a writing error prevented the function from completing. In such cases, the error indicator (accessible through `ferror`) for the file stream may be set.
- If either size or count is zero, the function returns zero and both the stream state and the content pointed by ptr remain unchanged.


### `size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream)`

- **Returns**: The total number of elements successfully written.
- Writes data from the memory pointed to by `ptr` to the file specified by `stream`.
- If the return value differs from the `count` parameter, it indicates a writing error prevented the function from completing. In such cases, the error indicator (accessible through `ferror`) for the file stream may be set.
- If either size or count is zero, the function returns zero and both the stream state and the content pointed by ptr remain unchanged.

### `int fgetc(FILE *stream)`

- **Returns**: ASCII value of the character on success, EOF on failure.
- Reads characters from a file one by one.

### `void fputc(int c, FILE *stream)`

- **Returns**: The character written on success, EOF on failure.
- Writes characters from a file to the console or another file.

### `char *fgets(char *str, int n, FILE *stream)`

- **Returns**: The `str` parameter/arguments on success, NULL on failure.
- Reads a line from the specified `stream` and stores it in the string pointed to by `str`.
- Stops when either (n-1) characters are read, the `\n` is read, or the end-of-file is reached, whichever comes first.
- Retains `\n` unlike `gets`.

### `int fputs(const char *str, FILE *stream)`

- **Returns**: Non-negative value on success, EOF on failure.
- Writes a string to a file. Does not append a new line unless specified.

### `int fprintf(FILE *fp, const char *format, ...)`

- Works exactly like `printf()` but writes to a file.

### `int fscanf(FILE *fp, const char *format, ...)`

- Works exactly like `scanf()` but reads from a file.

### `int feof(FILE *stream)`

- **Returns**: Non-zero if the end of the file is reached, 0 otherwise.
- Checks whether the end-of-file (**EOF**) indicator has been set for the specified file stream (if the end of the file has been reached), it does not examine the associated data source.
- In typical usage, input stream processing stops on any error; `feof()` and `ferror()` are then used to distinguish between different error conditions. 
- The `feof` function is often used in conjunction with other file input functions like `fgetc`, `fgets`, or `fread` to determine if you have read all the data from a file. It helps prevent reading beyond the end of the file, which can result in unexpected behavior.
- For example, if the most recent I/O was a `fgetc`, which returned the last byte of a file, `feof` returns **zero**. The next `fgetc` fails and changes the stream state to end-of-file. Only then `feof` returns **non-zero**.
### `int ferror(FILE *stream)`

- **Returns**: Non-zero if there is an error, 0 otherwise.
- Differentiates between errors and EOF.

### `int fseek(FILE *pointer, long int offset, int position)`

- **Returns**: 0 on success, non-zero on failure.
- Moves the file pointer to a specified position.
- `pointer`: Pointer to a `FILE` object that identifies the stream.
- `offset`: Number of bytes to offset from the specified `position`.
- `position`: Defines the point with respect to which the `offset` is added. It has three values:
    - `SEEK_SET` **(or 0)**: Denotes the beginning of the file.
    - `SEEK_CUR` **(or 1)**: Denotes the file pointer's current position.
    - `SEEK_END` **(or 2)**: Denotes the end of the file.
### `long int ftell(FILE *stream)`

- **Returns**: The current value of the position indicator (file pointer) or **-1L** if an error occurs. The global variable `errno` is set to a positive value in case of an error.
- Returns the current position of the file pointer.

# Miscellaneous Functions for Files

### `int rename(const char *oldname, const char *newname)`

- **Returns**: 0 on success, non-zero on failure.
- Renames a file.

### `int remove(const char *file_name)`

- **Returns**: 0 on success, non-zero on failure.
- Erases a file.

### `void rewind(FILE *fp)`

- Positions a file's current location to the start of the file.
- Equivalent to `fseek(stream, 0L, SEEK_SET)` but also clears the error indicator for the stream. `fseek()` is preferred over `rewind()`.
- can be useful to find the file size with `ftell()`.
