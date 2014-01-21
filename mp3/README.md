# Setup

Copy the mp3.cu file into the current directory and unzip the dataset.

    make setup

Then edit the Makefile. Uncomment the appropriate section, depending on whether you 
are running on a GPU card or using the Ocelot emulator.


# Compiling and Running

Build the mp3 executable.

    make

Run the program and display the results.

    make tests

This will run all 10 tests. You'll need to scroll back to see the individually.

To run just a single test, use a commands like this:

    make test n=0
    make test n=5
    make test n=9

The number is the test number (0 through 9).
