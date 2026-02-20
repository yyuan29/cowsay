# lab - pip install and PEP8

![](https://github.com/mikeizbicki/lab-cowsay/workflows/flake8/badge.svg)&nbsp;
![](https://github.com/mikeizbicki/lab-cowsay/workflows/command_line/badge.svg)&nbsp;

**About:**
This lab will have you practice installing python libraries and running *linters*.
You will need to understand this material to get the github actions to pass on your markdown compiler homework.

## Part 0: setup

For this lab you will need to make a copy of this repo on github.
Follow the standard procedures to create a new empty repo through the github interface,
clone this repo onto your computer,
and then push to your new empty repo.

Each part below will have you pushing to your new repo to fix parts of the github actions,
so you'll need to get this repo setup before continuing.

## Part 1: pip

This repo contains a script that shows a cow saying a message:
```
$ python3 cowsay/__main__.py 'mooooo moooo'
 ______________
| mooooo moooo |
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
$ python3 cowsay/__main__.py 'hello world'
 _____________
| hello world |
 -------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
It's a bit cumbersome to always have to type out `python3 cowsay/__main__.py` whenever we want the cow to say something.
So python gives is a tool called `pip` that allows us to *install* packages into an easier-to-use form.
Try running the command
```
$ pip3 install .
```

> **NOTE:**
> Depending on your computer's configuration,
> you might get a scary error message that looks something like
> ```
> error: externally-managed-environment
>
> × This environment is externally managed
> ╰─> To install Python packages system-wide, try apt install
>     python3-xyz, where xyz is the package you are trying to
>     install.
>
>     If you wish to install a non-Debian-packaged Python package,
>     create a virtual environment using python3 -m venv path/to/venv.
>     Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
>     sure you have python3-full installed.
>
>     If you wish to install a non-Debian packaged Python application,
>     it may be easiest to use pipx install xyz, which will manage a
>     virtual environment for you. Make sure you have pipx installed.
>
>     See /usr/share/doc/python3.12/README.venv for more information.
> note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
> hint: See PEP 668 for the detailed specification.
> ```
> Python recently made the install procedure a bit more complicated in order to prevent something called [dependency hell](https://en.wikipedia.org/wiki/Dependency_hell).
> Unfortunately, this makes setup harder for new programmers.
>
> To fix the issue, you have to create a `venv`.
> (The first "v" standands for "virtual" and you will hear people pronounce `venv` as either "virtual environments" or just "venvs".)
> A `venv` is a project-specific installation point,
> and it allows every project to have its own libraries installed.
>
> Setup a venv for this cowsay project by running the following command:
> ```
> $ python3 -m venv venv
> ```
> Notice that this creates a new `venv` folder in your working directory.
> Then *activate* the venv with the command
> ```
> $ source venv/bin/activate
> ```
> You should see your prompt change to include the string `(venv)` somewhere inside of it.
>
> Now you should be able to run the install command without any error:
> ```
> $ pip3 install .
> ```
>
> When working with python projects, you only run the `python3 -m venv venv` command once.
> But you have to run the `source venv/bin/activate` every time you close and reopen VSCode.
>
> Every programming language has problems with managing installed libraries, but python is particularly notorious for having lots of difficulties.
>
> <img src=img/money.jpg width=300px>

After you have successfully installed your project, you can use the `cowsay` command in the shell:
```
$ cowsay 'moo'
 _____
| moo |
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
And you can use this command from any folder
```
$ pwd
/home/user/proj/lab-cowsay
$ cd .. # always takes you to the "parent" folder; observe how pwd changes
$ pwd
/home/user/proj
$ cowsay moo
 _____
| moo |
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
$ cd lab-cowsay
$ pwd
/home/user/proj/lab-cowsay
```
In your last lab, you installed the yt-dlp package from github by first cloning and then running the script manually.
It is far more common in the python world to install packages like yt-dlp via pip.
You can install the yt-dlp library with:
```
$ pip3 install yt-dlp
```
Notice that if we put a *package name* after the `pip3 install` command, we do not have to clone it;
pip will do all that work for us automatically.

Now you should be able to run `yt-dlp` whenever you want in your terminal to download fun videos and watch them without ads.
```
$ yt-dlp 'https://www.youtube.com/watch?v=XfELJU1mRMg'
```

> **Fun Aside:**
> Pip stands for "Pip installs packages".
> This is called a *recursive* acronym because the acronym contains itself.
> These recursive acronyms are quite popular in programming.

**Your Task:**

The `command_line` github actions is failing for this repo because the action tries to run the `cowsay` command without first installing it via pip.
Follow the instructions in the `.github/workflows/command_line.yaml` so that the action passes.

## Part 2: PEP8 and flake8

<img src=img/guido.png width=300px>

*Python Enhancement Proposals* (PEPs) are the system for adding new features to python.
The most famous PEP is [PEP8](https://peps.python.org/pep-0008/),
which defines best practices for formatting python code.
For example, in python, it is recommended to put spaces around operators.
Thus the following code
```
x=1+2
```
is considered "ugly" and should be rewritten as
```
x = 1 + 2
```
to conform to PEP8.

It is common for python programmers to run tools called *linters* that enforce PEP8 formatting.

> **NOTE:**
> The name *linter* comes from the idea that clothing with lint on it still serves its purpose, it's just ugly.
> Similarly, python code that is not formatted according to PEP8 still works, it's just ugly.

The most famous linter is called `flake8`.
You can install it with pip by running
```
$ pip3 install flake8
```
Then you can lint the cowsay code with the command
```
$ flake8 cowsay
cowsay/__main__.py:8:19: E201 whitespace after '('
cowsay/__main__.py:8:49: E202 whitespace before ')'
cowsay/__main__.py:9:1: W293 blank line contains whitespace
cowsay/__main__.py:12:23: E225 missing whitespace around operator
cowsay/__main__.py:13:1: W293 blank line contains whitespace
cowsay/__main__.py:14:23: E225 missing whitespace around operator
cowsay/__main__.py:24:1: W293 blank line contains whitespace
cowsay/__main__.py:25:23: E225 missing whitespace around operator
cowsay/__main__.py:26:1: W293 blank line contains whitespace
cowsay/__main__.py:33:1: W293 blank line contains whitespace
cowsay/__main__.py:42:1: W293 blank line contains whitespace
```
Each line of the output shows a violation of PEP8 formatting.

**Your Task:**

The flake8 github action runs this linter and fails if there are any violations of PEP8 style.
To make the test case pass, you will have to modify the file `cowsay/__main__.py` so that `flake8` does not return any linting errors.

## Submission

Ensure that all github actions badges are green.
Then submit your repo link to canvas.
