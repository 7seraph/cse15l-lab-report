# Lab 1 - Remote Access and File System
---
## cd
The `cd` command is known as to 'change directory' in the Terminal. Similar to double clicking and navigating with a mouse, one can navigate with the Terminal with `cd <path>`. 

**What if you use `cd` without any `<path>` or argument?**
- Say for example you open up the terminal and simply type `cd` with no path. You'll get something similar to this:
```
[user@sahara ~]$ cd
[user@sahara ~]$
```
> In this case, if you use the `cd` command without any path followed after the command in no directory...then nothing happens and the terminal prompts the user to provide an input. 

**What if you want to use `cd` to a directory as an argument?**
- Say for example your file structure is `home-->Downloads-->cse15l-->hello.java` and you are currently at the `home` directory. However, you want to get to the `Downloads` directory.
```
[user@sahara ~]$ cd Downloads
[user@sahara ~Downloads]$
```
> You see that `cd Downloads` means that we are changing the directory to `Downloads` and you will know that it worked sucessfully once the prompt changes. This is where you see that `user@sahara -]` changes to `[user@sahara ~Downloads/]`. Now, we have moved to the `Downloads` directory and access files that are specifically in that file. (More on that when we go over the `ls` command).

- Now let's say that you are in the `Downloads` directory and then use the `cd` command. Let's see what will happen:
```
[user@sahara ~]$ cd Downloads
[user@sahara ~Downloads]$ cd
[user@sahara ~]$
```
> Notice how `cd Downloads` changes the current directory to `Downloads` and once we use the `cd` command after with no path or argument, we would not be in a directory. 

- Here is one example where we are in 2 directories and we use `cd` without any path or argument:
```
[user@sahara ~]$ cd Downloads
[user@sahara ~Downloads]$ cd cse15l
[user@sahara ~Downloads/cse15l]$
```
> We used the `cd` command to change directories into the `Downloads` directory. Then we used the `cd` command a second time to change directories from `Downloads` to `cse15l`. When we use the `cd` command with no path or argument in the `cse15l` directory, the prompt exits out of all directories. Simply put, we are not in any directory (we've exited out of the `cse15l` directory and the `Downloads` directory.

**What if you want to use `cd` to a file as an argument?**
- Let us take the same file structure from before (and that we are in the `home` directory) but in this case, you want to get to the `hello.java` file.
```
[user@sahara ~]$ cd Downloads/cse15l/hello.java
bash: cd: hello.java: Not a directory
```
> Note that `cd Downloads/cse15l/hello.java` resulted in an error message because `hello.java` is a file and not a directory.

Therefore, we can navigate to the closest directory to the file by doing:
```
[user@sahara ~]$ cd Downloads/cse15l
[user@sahara ~Downloads/cse15l]$
```
> This would not give us an error because `cse15l` is a directory, not a file. Alternatively, you could type in the terminal `cd Downloads` and then `cd cse15l` separately.

## ls
The `ls` command is known as "list", where the command will provide a list of all the files **and** directories under the directory that the prompt is under. 

**What if you use `ls` without a `<path>` or argument?**
- Say for example that our file structure is the same as before and that we are at the home directory where `home-->Downloads-->cse15l-->hello.java`.
```
[user@sahara ~]$ ls
Downloads
[user@sahara ~]$
```
> Note that `ls` can work without a `<path>`. If there is no path associated, then the command will return a list of all files and directories of whichever directory the prompt is currently under. In this case, we were given a list of all the visible files and directories when we are in the `home` directory. `Downloads` is the only directory that we see. Also, since `Downloads` is a directory, the color of the text is different than a file (see next example).

**What if you use `ls` with a `<path>` to a directory as an argument?**
- Say for example that we are in the home directory and we want to see what files and directories are in the `Downloads` directory. That is, what files and directories are in the `Downloads` directory?
```
[user@sahara ~]$ ls Downloads
cse151l  hello.java
[user@sahara ~]$
```
> The terminal will return a list of the files and directories in the `Downloads` directory. Note that `cse15l` will be in a different colored text compared to `hello.java`. The reason for this is because `cse15l` is a directory whereas `hello.java` is a file. 

**What if you use `ls` to with a path to a file as an argument?**
- Say for example that we are in the home directory and we want to use `ls` with the path to the `hello.java` file. Using the same idea with `cd`, we would have to include the path to the file.
```
[user@sahara ~]$ ls Downloads/cse15l/hello.java
Downloads/cse15l/hello.java
[user@sahara ~]$
```
> Note that the terminal will return the path if the argument is a path to a file. There is nothing else for `ls` to list if the file is an executable file (`hello.java` in this case; .txt files would also count as an executable file).

## cat
The `cat` command is a shorthand name for "concatenate". While one might think that this command would combine files or directories together, `cat` reads the file and returns the contents of the file.

**What if you use `cat` with no arguments?**
- Let us say that the file structure is the same as before `home-->Downloads-->cse15l-->hello.java` and we are in the home directory.
```
[user@sahara ~]$ cat
1
1
2
2
3
3
^C
[user@sahara ~]$
```
> When the command `cat` runs without an argument, the prompt disappears and the terminal is waiting for user input. In this case, 1 was entered **once** but it appears twice. When 2 is entered once, it appears once more. The same goes when 3 is entered. What happens here is that the `cat` command is reading the user input and returning it back (printing) to us. Also note that this is a loop and continues unless the user hits `CTRL+C` (Windows) to exit out the loop.

**What if you use `cat` with a path to a directory as an argument?**
- With the same file structure as before, let us try to use the command onto Downloads.
```
[user@sahara ~]$ cat Downloads
cat: Downloads: Is a directory
[user@sahara ~]$
```
> Note that the command did not print out anything but the error message that `Downloads` is a directory whereas the command `cat` deals with reading files (and not directories).

**What if you use `cat` with a path to a file as an argument?**
- Let us say that we want the command to read and return the contents that are in `hello.java`. We can do so either by:

1) changing the directory with the path to the file, then using the `cat` command to the file as the argument
```
[user@sahara ~]$ cd Downloads/cse15l
[user@sahara ~Downloads/cse15l]$ cat hello.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);
    System.out.println(content);
  }
}[user@sahara ~]$
```
2) or include the path to the file without changing the directory as the argument
```
[user@sahara ~]$ cat Downloads/cse15l/hello.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);
    System.out.println(content);
  }
}[user@sahara ~]$
```
> Both work but the key idea is that `cat` will read and return the contents of a file, not a directory.
