# Lab 1 - Remote Access and File System
---
The `cd` command is known as to 'change directory' in the Terminal. Similar to double clicking and navigating with a mouse, one can navigate with the Terminal with `cd <path>`. 

**What if you use `cd` without any `<path>` or argument?**
- Say for example you open up the terminal and simply type `cd` with no path. You'll get something similar to this:
```
[user@sahara -]$ cd
[user@sahara -]$
```
Simply put, if you use the `cd` command without any path followed after the command...then nothing happens and the terminal prompts the user to provide an input.


**What if you want to use `cd` to a directory as an argument?**
- Say for example your file structure is `home-->Downloads-->cse15l-->hello.java` and you are currently at the home directory. However, you want to get to the `Downloads` directory.
```
[user@sahara -]$ cd Downloads
[user@sahara ~Downloads/]$
```
> You see that `cd Downloads` means that we are changing the directory to `Downloads` and you will know that it worked sucessfully once the prompt changes. This is where you see that `user@sahara -]` changes to `[user@sahara ~Downloads/]`. Now, we have moved to the Downloads directory and access files that are specifically in that file. (More on that when we go over the `ls` command).

**What if you want to use `cd` to a file as an argument?**
- Let us take the same file structure from before but in this case, you want to get to the hello.java file.
```
[user@sahara -]$ cd Downloads/cse15l
[user@sahara ~Downloads/cse15l/]$
```
> Note that if we tried `cd Downloads/cse15l/hello.java` we would get an output: `hello.java is not a directory` because hello.java is a file.
