tags: #intro

## Main message
Structure your files and packages in an intuitive and thought out way that either represents the physical systems or the delineation of people using the files.

## What kind of folder structure do I need to make a Python package?
It's pretty easy, you basically need:
- a setup.py file
- a folder with the name of the package you want
- anything to ever get imported must live in that package; otherwise it's outside of it
- top-level files are usually READMEs, docs, [[CI]]

## There are some requirements for Python packages
- what I mean by a Python package is that you can install and import it. The next levels are pip and conda
- it's probably easiest to start from an existing package
- but once you make a few you get the hang of it
- do just start from an existing package with approximately the same complexity as yours

