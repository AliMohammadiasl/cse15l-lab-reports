# Lab 1 Report

### Using the `cd` command
![Image](Lab1CD.png)

![Image](Lab1CD2.png)

I tried using `cd` on its own and it did nothing as we did not give it a directory to switch to. This not an error because we just did not give it any directory to switch to. The point of the `cd` command is to change the directory of our code, hence why it is called "cd".
Then I tried `cd lecture1` which switched the directory to lecture1. That is because we specified a directory that we want to change to. 
Then when I tried using `cd` to a file, it gave an error saying that it is not a directory. The whole function of `cd` is to change directory, therefore, it will not work on a file. Thereafter, I tried the `cd` command with no arguments on my home page. It didn't do anything. Then I tried to change the directory and go to `lecture1/messages` and then run cd. This time it returned me to my home directory. Basically, if we are on a different working directory than our home one, and we try to run `cd`, it will just bring us back to our home directory. Again, notan error as that is what it is supposed to do (return to home).


***
### Using the `ls` command
![Image](Lab1LS.png)

![Image](Lab1LS2.png)

When usinf the `ls` command by itself, it showed the names of the files and folders inside the current directory.
When using `ls lecture1`, it gave an error because we are currently inside lecture 1.
When using `ls messages/en-us.txt` it just shows `messages/en-us.txt` because that is the only file at that location. 
Then I tried using `ls lecture1` while I was inside the home directory. This time, using the correct path and not being inside the `lecture1` directory, the console returned whatever is inside `lecture1`. Then I did the same thing for `messages` but I made sure to `cd` to `lecture1` because that is where the `messages` folder is located. 

***
### Using the `cat` command
![Image](Lab1Cat.png)
When using `cat` by itself, it keeps us stuck within the command until we enter `^C` aka Ctrl C. That is actually not an erro although it might seem like it. The way it behaves when we initally run it with no argument, then give it arguments, is that it returns the argument. When using `cat` without any argument, it will read data from its standard input and write it to its standard output, which I can't think of a use for. 
When using `cat lecture1` while we are in our home directory, we get a message saying `lecture 1 is a directory`. That is an error because concatenating a directory is not possible. 
Wheb using `cat Hello.java` it displays the contents of Hello.java. 
The `cat` command basically shows the contents of a file and does not work on a directory. 
