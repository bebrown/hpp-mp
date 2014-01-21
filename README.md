# Introduction

This is a local development environment for the Heterogeneous Parallel Programming course.
You may use this to write and test the programs for the class. You will need to be familiar
with using a Linux command line to be successful. This is an Ubuntu 12.04 LTS stock distribution,
but with extraneous packages removed to save space. It has a web browser, compiler, and that's
about it.

There are several directories here: mp0, mp1, mp2, etc. Each one corresponds to a program
you need to write in theclass. In each directory there is a README file that contains instructions
for setting up, compiling, and running each program. What is not explained, however, is how to
edit the files; this is where your familiarity with command-line development will come in handy.

You can use a command line editor such as vi/vim or nano. Or you can use a GUI editor such as
gedit.

In general, to compile a program just type `make`. And to test it, type `make test` or
`make tests` (depends on the assignment).

# Updating

Changes to the Makefile and test suite are released occasionally. Please update the files by
pulling the latest changes from the GitHub repository.

    git pull

This will update all the files.

