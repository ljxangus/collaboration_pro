# DARPA Spectrum Collaboration Challenge Collaboration Protocol

## Introduction
This repository contains the Collaboration Protocol interface specification along with supporting 
documentation. 

The repository documentation is stored in a mix of HTML and Markdown (.md) files. The HTML files are 
autogenerated documentation for the Protocol Buffer interface specifications. The HTML can be viewed 
by first downloading them and opening them using any standard web browser. GitLab will not render
them natively.

The .md files (such as this one) can be viewed directly on GitLab, where they will be rendered in 
a more human readable view, including clickable links and inline images. To view these files
in a local clone of this repository, use a markdown format previewer or a web browser plugin such 
as Markdown Preview Plus on Google Chrome.


## Repository Layout
The root of the repository contains the interface specification as a Google Protocol Buffer 
.proto file. It also contains the following subdirectories:

*   [doc](doc) This contains any autogenerated documentation built from code in this repository

*   [examples](examples/README.md) This contains runnable examples illustrating how to work with the 
    Collaboration Protocol

*   [scenarios](scenarios/README.md) This contains a series of scenarios showing the ways in which 
    the messages in the Collaboration Protocol may be used. Any time new messages or data types are 
    added to the Collaboration Protocol, there should be a new scenario added in its own 
    subdirectory to illustrate how and why the new messages would be useful. Diagrams are 
    encouraged.
