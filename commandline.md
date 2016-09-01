To start, type the following command and hit enter.


 ```sh
hostname
```

```sh
whoami
```

Much like using your finder, at any point when working in the terminal, you are associated with a particular directory. 
To see which director you are in, type:

```sh
pwd
```

To see all of the files and subdirectores, type:

```sh
ls
```
Commands that we run in the terminal often have options that change their behavior. A common one for the `ls` command is:

```sh
ls -l
```

What do we see?
It stands for list-long.

To change where we are in the file system, we use the very important command, your best friend! Type `cd` followed by where you want to go. 

 
```sh
cd Desktop
```
Now pick another directory to move into. 

Now let's back up! Let's say I want to go back to the previous directory. We can use `cd ..`. 

You can also give it the complete file name. For example, another way to get where we are now would be the following:

```sh
cd /Users/YOURUSERNAME/Desktop
```
Make sure to put your username. The advantage is that this approach works regardless of where you are in the terminal. 

A lot of things you can do pointing and clicking on your computer you can do here! Let's say we wanted to add a new folder on our desktop.

```sh
mkdir NAME
```
Can you see the new director using the `ls` command?
Now look on your desktop. Can you see it?

So maybe we don't actually want this directory. No problem! Let's remove it. 

```sh
rmdir NAME
```
Let's use `ls` command again. Do you see your directory?

Did you know your computer can talk to you? Type:
```sh
say i love digital humanities
```

But wait, I want a different voice!
We have some options: [Voices](http://www.gabrielserafini.com/blog/2008/08/19/mac-os-x-voices-for-using-with-the-say-command/)

Try a few! 

A few other things of interest:

```sh
top
```
We can see our machine working! To get out, type `q`.

