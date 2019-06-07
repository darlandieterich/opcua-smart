# OPC-UA Ruby Bindings (open62541)

The development of OPC UA applications takes currently a lot of effort. This is caused by the large possibilities of the OPC UA specification. With this implemtation we want to define some conventions, which shoud make the technology more useable.

## Table of Contents

1. [Installation](#Installation)
2. [Examples](#Examples)
    1. [Server](#Server)
    2. [Client](#Client)

## Modelling Style

TBD

## COPYING

Copyright (C) 2019-* Jürgen "eTM" Mangler <juergen.mangler@gmail.com>. opcua-smart is freely distributable according to the terms of the GNU Lesser General Public License 3.0 (see the file 'COPYING'). This code is distributed without any warranty. See the file 'COPYING' for details.

## Installation

Dependency: https://github.com/open62541/open62541 > 0.4 (master branch as of 2019-04-26)

```sh
git clone https://github.com/open62541/open62541.git
cd open62541
mkdir build
cd build
cmake ..
ccmake ..
# Configuration, see picture below
make
sudo make install
gem install opcua
```

![ccmake Config](config.png)

If the installation works correctly, but examples are still complaining about missing lib62541.so, try this:

```sh
sudo echo "/usr/local/lib" > /etc/ld.so.conf.d/local.conf # add to libs path
sudo ldconfig # update libs
sudo ldconfig -p | grep libopen62541 # check if its there
```

## EXAMPLES

### Server

The server has following steps:
* Create the server and add_namespace
* Create ObjectTypes
* Manifest ObjectTypes
* Loop for getting real life data

#### Create server and namespace

```ruby
server = OPCUA::Server.new
server.add_namespace "https://yourdomain/testserver"
```


#### Create ObjectTypes -- Defining an information model

We decided, that it 

```ruby
to = server.types.add_object_type(:TestObjectType).tap{ |t|
  t.add_variable :TestVariable
  t.add_object(:TestObject, server.types.folder).tap{ |u|
    u.add_object :M, mt, OPCUA::OPTIONAL
  }
  t.add_method :TestMethod, inputarg1: OPCUA::TYPES::STRING, inputarg2: OPCUA::TYPES::DATETIME do |node, inputarg1, inputarg2|
    #do some stuff here
  end
}
```
In this example the _TestObjectType_ is defined. It consits of _TestVariable_ of the _BaseVariableType_ an _TestObject_ of the _FolderType_ and a _TestMethod_. The ``` .add_variable :TestVariable ``` command adds a variable.


### Client
TBD. See examples subdirectory.
