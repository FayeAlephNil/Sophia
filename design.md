# Sophia Design Doc
This is the design document for the sophia package manager for the Emily programming language (emilylang.org). This will be written in Python and will be as modular as possible.

## Storage
Packages would be stored in a central git repository. This repository would essentially be a list of metadata json files that would contain the following information
  * name
  * source
    * version-key
    * url (url to use with method)
    * method (git or similar)

## Naming
Packages can be named anything, however there are two rules for naming packages
  1. The "first element" in the package name, should be controlled by a specific person or organization who registers it
  2. nobody should ever check in a package whose path corresponds to a file in another repo

For example, it's ok for there to be a package emily.ffi.cpp, and a package emily.ffi.cpp.clang as long there's no clang file in emily.ffi.cpp

These rules are not enforced by Sophia! They are social rules and not adhering to them is bad practice.

## Dependency Installation
Dependencies will install to one of two places. If they are local dependencies they will install to .emilylocallibs in the project folder. If they are global dependencies then they will install to ~/.emilylibs. They will also install with a metadata file called \_package.json which will be a clone of the metadata file in the central repo

## Sophia dependency file
This file declared as name.sophia where name is variable will describe the dependencies of the project. It will a json file that stores the names of dependencies, their versions, and whether they are local or global.

## Sophia Commands

* get - Installs a single package based on a name (takes --local or --global)
* getAll - Installs the packages specified in the .sophia file (takes --local or --global)
* build - builds a sophia projects dependencies installing them all locally (in .lib) so you can zip up your project and give it to an end-user and they don't need to run ```sophia getAll```
* run - this will run a library. This works by checking the library for a main.em file in the library and running it if it exists

## Usage in Programs

@mcclure if you could look at this for implementing into Emily that would be appreciated
