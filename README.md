# Rust Guide

The rust guide is a collection of rust primers and tutorials made for 
CS23500: Intro to Database Systems at the University of Chicago. 

The guide is hosted at [uchi-db.github.io/rust-guide/](https://uchi-db.github.io/rust-guide/README.html)

The guide is made using Myst markdown and is hosted on GitHub pages.

## Dependencies
Create a python virtual environment, and install the required packages
```bash
python -m venv .venv
source ~/.venv/bin/activate
pip install -r requirements.txt
```

## Building
To build and serve this guide locally:
```bash
jupyter-book build docs
```

## Github Page Deployment
Any pushes to the main branch of this repository will automatically trigger 
a build-and-deploy action to update the webpage.

## Contributing
If you discover a typo, or inconsistency, please report an Issue or create a Pull request 
in this repository.
