# `sheclang` - A `#!` for your C++ files.
## Installation & Test
To install, just stick the bash script in your path either by a copy or a symlink.
```
git clone https://github.com/lrenaud/sheclang
cd sheclang
sudo cp -v sheclang /usr/bin/
```
To run, try the demo after installing.
```
chmod +x ./hello-world.cpp
./hello-world.cpp
```
## Use
### Basic Use
1. Add the following line to the first line of your C++ file.
```
#!/usr/bin/env sheclang
```
2. Mark your top level `*.cpp` file as executable
```
cd ~/your-project
chmod +x your-source-code.cpp
```
3. Run the source file like it was an executable. Arguments passed to the `*.cpp` file will be forwarded onto the resulting binary directly.
```
./your-source-code.cpp --your-argument positional --this-flag
```
### Advanced Use
 - Use the `env -S` seperator to pass build arguments directly into `sheclang`.
   - `sheclang` looks for the `--` as a seperator when invoked in this way to identify the arguments intended for the compiler verses arguments intended for your executable. If you do not want to have to play the game of complexities in the invocation here, consider using an environmental config to override the Magic Variables instead.
   - example: `#!/usr/bin/env -S sheclang -lm --` to pass the `-lm` flag directly to the compiler.
 - Use a `~/.config`, `~/.sheclang`, or local `sheclang.conf` to add compiler arguments
   - `sheclang` will look for files the following order, and simply source the contents of the files prior to doing any file processing, compiling, or executing.
     1. `$HOME/.config/sheclang/config`
     2. `$HOME/.sheclang`
     3. `$PWD/sheclang.conf`
     4. `$PWD/.sheclang`
   - If you want to override the configuration of a previous script, uses a higher numbered (later loaded) script to set the final configuration prior to the build process. For arugments you can override, look at the Magic Variables List section.

### Magic Variables List
The following variables are used internally by sheclang, and can be overriden by a sourced script as defined in the advanced usage.

| Variable | Default | Description |
| --- | --- | --- |
| `COMPILER` | clang++ | The compiler called by sheclang |
| `SHECLANG_VERBOSE` | false | When `true`, report information about the execution process for debugging |
| `POST_BUILD_FLAGS` | *empty array* | an array of flags to pass to `$COMPILER` at build time. |
| `PRE_BUILD_FLAGS` | *empty array* | an array of flags to pass to `$COMPILER` prior to the source code file. These are post-merged with arguments that are pased via an advanced `!#` call per the Advanced Use section above. |
| `RUNTIME ARGS` | *empty array* | Arguments passed to your executable. Automatically merged with things you pass when invoking the script. These arguments are placed before arguments passed via the CLI. |

## Why?
Because I could. And anything that makes building performant software more
assessable to more users is worth it. I can't imagine many Python beginners are
using the debugging facilities and interactivity of the Python interactive
terminal. So why not do what I can to make building C++ as trivial to get
off the ground as trivial python. I detest build systems, and I just want my tools
to work.
