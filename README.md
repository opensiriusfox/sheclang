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
## Why?
Because I could. And anything that makes building performant software more
assessable to more users is worth it. I can't imagine many Python beginners are
using the debugging facilities and interactivity of the Python interactive
terminal. So why not do what I can to make building C++ as trivial to get
off the ground as trivial python.