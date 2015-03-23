# rpmdeptree
Show the missing dependencires for a specified pm package in a tree view

#Introduction

The `.rpm` packaging technology is adopted by many Linux distributors like Red Hat, Fedora, CentOS. 

Normally if our computer has been installed with the above list operating systems and we want to download or update a software, we need to use `yum install <package name>` or `yum update <package name>` to do so given that our computer is connected to a yum server. The `yum` command line utility will help you solve the dependency issue that this `.rpm` packaging technology will normally face.

But when your computer don't have a yum repository yet or you need to install a package that lack dependencies on yum server, you need to search the web to download the dependencies for your software manually. This process is always tedious because you don't know what dependencies are you lacking of from the "bottom of the tree".

While `rpmdeptree` can give you a clear view of this "tree"

#What is `rpmdeptree`?

`rpmdeptree`, short for "rpm dependency tree",  is a command line tool that can give you a "tree" view of the required dependencies for a given rpm package whenever the dependency is missing or existing in the current directory. The "current directory" here means the directory where the rpm package you want to install locates.

#Usage

1. `cd` to the directory where you packages locate
2. use `rpmdeptree <package name>` to see the result

You could also see the detailed usage info with `rpmdeptree -h`

```bash
[tmp]$ rpmdeptree -h

    Usage:
        1. rpmdeptree package1 [package2 package3 ...]
        2. rpmdeptree *


    options:
        -h, --help : print this help page
        -l, --list : list the rpm files with chosen architectures(e.g. x86_64) (others not avaliable yet)

Done
```

##Example

You have `git-1.7.1-2.el6_0.1.x86_64.rpm` in your `git` directory

```bash
   [git]$ ls
   git-1.7.1-2.el6_0.1.x86_64.rpm
```

And you want to check what dependencies are lacking. You could use:

```bash
    [git]$ ls
    git-1.7.1-2.el6_0.1.x86_64.rpm
    [git]$ rpmdeptree git-1.7.1-2.el6_0.1.x86_64.rpm
    |
    |-git-1.7.1-2.el6_0.1.x86_64.rpm
        |
        |-perl-Git = 1.7.1-2.el6_0.1 (is needed)
    ----------------------------------------
    Done
```

You will know `perl-Git = 1.7.1-2.el6_0.1` is needed. So you need to download and install `perl-Git = 1.7.1-2.el6_0.1` first before you could install `git-1.7.1-2.el6_0.1.x86_64.rpm`.

#Install

1. Download the `rpmdeptree` file to your local computer
2. move the `rpmdeptree` file to under whatever dirctory that your `$PATH` variable shows, preferably in `/usr/local/bin`

Then you could feel free to use it. 

No:e, this version only work with package with architecture of `x86_64` currently.
