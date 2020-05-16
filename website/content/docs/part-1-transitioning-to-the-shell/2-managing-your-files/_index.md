---
title: "Chapter 3 - Managing Your Files"
slug: "chapter-3-managing-your-files"
weight: 2
---

# Chapter 3 - Managing Your Files

Copying, moving, renaming and deleting files in a graphical user interface is normally fairly intuitive. Now we'll learn how to perform the same operations in a shell. Once you can organise your files, you are well on your way to being able to use the shell more effectively for day to day tasks.

Now that we know how to organise the files in our computer, we'll take a look at how to download files, create new files, preview the contents of files, open files, copy, move and delete files.

This chapter will introduce the `file`, `cat`, `less`, `touch`, `zip`, `unzip`, `cp`, `mv`, `rm`, `rmdir`, `mkdir`, `curl` and `wget` commands.

# Creating a Playground

Before we start copying, deleting, moving and renaming files, we should create a 'playground' area we can work in. We don't want you testing all of these commands out on your own personal files before getting started!

To help with this, I've created a zipped up folder which has a lot of files in it which we can use to play with. Now the file itself is available on the [effective-shell.com](https://effective-shell.com) website. We *could* open up a web browser, download the file, unzip it and then start from there, but this book is all about how to deal with every day tasks in your shell, so let's do it in the shell!

The playground zip file is available at [effective-shell.com/downloads/effective-shell-playground.zip](https://effective-shell.com/downloads/effective-shell-playground.zip). Rather then opening a browser to download it, let's do it with the shell.

Open your shell - if you've not yet got set up with your shell, that's OK, just check [Chapter 1 - Getting Started]({{< relref "/docs/1-getting-started" >}}).

Now that you have your shell open, we can run the `wget` command (_Web Get) to download the zip file. Let's download it to our Home folder. If you are not sure what the Home folder is, check [Chapter 2 - Navigating Your System)[{{< relref "/docs/2-navigating-your-system" >}}).

Here's the command to download the file to your Home directory:

```sh
wget 
```

You'll see something like this:

<img alt="Screenshot: wget" src="images/wget.png" width="800px" />

When you call the `wget` command, you can give it any web address and it'll download it to your current folder. But we might not be in our home folder when we call it, so to be on the safe side, we'll use the `-O` (output) flag to tell it explicitly that we want it downloaded to our home directory.

Let's look at our home directory now, with a quick call to `ls ~`:

<img alt="Screenshot: ls home" src="images/ls-home.png" width="800px" />

Cool - we have the zip file downloaded.

# Finding out about files

One of the interesting things you can do in a shell is ask it to tell you more about a file. This can be useful if we've got a file, and we're not sure what it might be. Let's try it out now:

```sh
file ~/effective-shell-playground.zip
```

<img alt="Screenshot: file" src="images/file.png" width="800px" />

Not the most interesting out outputs - it's basically telling us we have a zip file. But as we use it more we'll see how it can be quite powerful.

# Extracting the Zip

Right now we have a zip file. We need to extract it, unpack the files so that we can play with them. Again, in a system with a graphical user interface, this is easy, generally you just double click on it. But we're going to use the shell for this!

Run the command:

```sh
unzip ~/effective-shell-playground.zip
```

Now let's look at what we've got with the `ls` command:

<img alt="Screenshot: unzip" src="images/unzip.png" width="800px" />

Excellent - we've now got a _folder_ which contains all of the files in the zip archive.

# Deleting Files

Now that we've downloaded and unzipped the file, we don't need the zipped version any more. So let's delete this file.

The `rm` (_Remove_) command can be used to delete a file. If we run:

```sh
rm ~/effective-shell-playground.zip
ls
```

Then we'll see the following:

<img alt="Screenshot: rm" src="images/rm.png" width="800px" />

Notice that the zip file is gone - just the folder is left.

By the way - be really careful with the `rm` command. Unlike in a graphical interface, it won't put files you delete into a recycle bin, they are blatted forever. One little thing it _will_ do to try and help you not make mistakes is let you know if you are trying to delete a whole folder.

Run the following command to try and delete the unzipped folder:

```sh
rm ~/effective-shell-playground
```

<img alt="Screenshot: rm error directory" src="images/rm-error-directory.png" width="800px" />

The `rm` command has not run in this case - it's warning us that we're not deleting a file, but a whole directory.

Now we can get around this by adding the `-r` flag, which means 'recursive' - i.e. not just the folder but everything in it. But use this with caution!

# Examining the Contents of a Folder

Let's take a look at what is in the playground. By the way, the output you might see here might have a few more files in it as I might have added some after writing this article!

In a graphical user interface, we'd open the folders and look at the files. In the shell, we can use the `tree` command to show the contents of a folder.

Try it out with:

```sh
tree ~/effective-shell-playground
```

<img alt="Screenshot: tree" src="images/tree.png" width="800px" />

The `tree` command shows you all of the folders and files in a location. If we are unsure what one of the files is, we can ask the shell to give us more info. For example, I could find out more about the `loas-gch.JPG` file by running:

```sh
file ~/effective-shell-playground/pictures/loas-gch.JPG
```

<img alt="Screenshot: file info for JPEG file" src="images/file-jpeg-info.png" width="800px" />

Note that the `file` command is already showing it is a bit more clever. It knows that the file is a `JPEG` file (a picture), but is giving other details as well.

# Copying a File

Let's say we really love that photo, and we want to make a copy of it. We can do that easily by using the `cp` (_Copy) command:

```sh
cp ~/effective-shell-playground/pictures/laos-gch.JPG ~/effective-shell-playground/pictures/laos-gch-copy.JPG
```

This makes a copy of the file - if you are not sure if it has worked, just run:

```sh
tree ~/effective-shell-playground
```

<img alt="Screenshot: cp command" src="images/cp.png" width="800px" />

We can see we've made a copy.

# Saving Some Keystrokes

Wow, it's painful putting `~/effective-shell-playground` before everything! From Chapter 2 we already know how to change directory, so let's do that now:

```sh
cd ~/effective-shell-playground
```

Excellent - until we tell our shell otherwise, this our new working directory.

# Renaming or Moving Files

Now I might be being a bit weird here, but I don't like how all of the photos have the ending `.JPG`, I prefer the lowercase `.jpeg`. So let's rename a file.

To do this, we use the `mv` (_Move_) command. When it comes down to it, moving a file or renaming a file amount to the same kind of operation, so one command can do both.

Rename the copy we made of the photo by running:

```sh
mv pictures/loas-gch-copy.JPG pictures/loas-gch-copy.jpeg
```

Let's run `tree` to see what happened. Remember - now that our working folder is the playground, we don't even need to tell `tree` where to look, if we give it no arguments it'll assume we're looking at the working directory:

<img alt="Screenshot: mv command" src="images/mv.png" width="800px" />

Much nicer! Now our copied file has been moved to have a new name. It's in the same folder still, but you can use `mv` to also change what folder a file is in.

# Creating a New Folder

Perhaps we're not happy with the name `pictures` for our folder we've been playing with, maybe we'd prefer to have them all in a folder called `photos`?

Probably the first thing we'd do in a graphical environment is create a new folder - so let's do thee same here!

Run the commands:

```sh
mkdir photos
tree
```

And we should see:

<img alt="Screenshot: mkdir command" src="images/mkdir.png" width="800px" />

We've use the `mkdir` command, which is short for _Make Directory_. This is how we create a new folder in the shell.

Now let's say we wanted to be _really_ organised, and create a photos folder by year and topic, perhaps `2019/outdoors/pictures`. In a graphical user interface, we'd have to create each folder one at a time. In the shell, it's easy!

```sh
mkdir -p 2019/outdoors/pictures
tree
```

Let's see how it looks:

<img alt="Screenshot: mkdirp command" src="images/mkdirp.png" width="800px" />

All we had to do was add the `-p` flag (which means "make the parent folder if it doesn't already exist) and we can create a whole set of subfolders. Now we're starting to see why knowing the shell can be powerful - if you know you have this trick up your sleeve you can be doing things like re-organising files _more effectively_ in a shell than in your graphical user interface!

# Deleting a Folder

Now that we have our more organise `2019/outdoors/photos` folder, we don't need the `photos` folder we created. So let's delete it! Remember how `rm` removes a file, and `mkdir` creates a folder? Well `rmdir` will remove a folder!

```sh
rmdir photos
tree
```

<img alt="Screenshot: rmdir command" src="images/rmdir.png" width="800px" />

As an important sidenote, just how `rm` doesn't move files to your recycle bin, so you cannot undo the operation, `rmdir` works the same way. So if we try to remove a directory which has things in it, such as the `pictures` directory, it will fail:

```sh
rmdir pictures
```

<img alt="Screenshot: rmdir fail command" src="images/rmdir-fail.png" width="800px" />

In this case, it is actually easier to just call `rm -r pictures`. Why is that? Well it's just like we saw in the earlier example - `rm` can delete files or directories. And if the directory is not empty, we just add the `-r` (_Recursive_) flag to tell it to delete the directory and everything it contains.


# Summary In this chapter we introduced the following: 
- The `pwd` (_print working directory_) command shows the current working directory
- The `$PWD` environment variable holds the current working directory
- The `ls` (_list) command shows the contents of the current directory or a given directory
- The `ls -l` command shows the contents of the current directory as list
- The `cd` (_change directory_) changes the current working directory
- Absolute paths are paths which specify the exact location of a file or folder...
- ...Relative paths are paths which are relative to the current directory
- The `.` special folder means 'this folder'
- The `..` special folder means 'the parent folder'
- The `~` special folder is the 'home directory'
- The `$HOME` environment variable holds the user's home directory
- You can run `cd` at any time to quickly go to your home directory
- You can use `pushd` and `popd` to push and pop the working directory stack
- You can use the `cd -` command to go back to the last location
