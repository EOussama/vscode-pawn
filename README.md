# vscode-pawn

Pawn tools for vscode.

Currently this is a port of the Sublime Text package which includes proper Pawn syntax highlighting, autocompletions for the standard library and some popular libraries.

Coming soon:

* Static Analysis
* Auto-complete
* Intellisense support

## Installation

Just search for "Pawn Tools" in the vscode extensions and install it.

## Compiling Pawn Code

Code uses a method called "Tasks" to run compilers and build tools. All you need to do is create a folder named `.vscode` in your project's directory and in there, create a file named `tasks.json` with the following contents:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build-normal",
            "type": "shell",
            "command": "${workspaceRoot}\\pawno\\pawncc.exe",
            "args": ["${relativeFile}", "-\\;+", "-\\(+"],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "isBackground": false,
            "presentation": {
                "reveal": "silent",
                "panel": "dedicated"
            },
            "problemMatcher": "$pawncc"
        }
    ]
}
```

`"command": "${workspaceRoot}\\pawno\\pawncc.exe",` is the important bit here, this is the path to your Pawn compiler and I've assumed most of you have a left-over `pawno` folder from that long dead text editor! This folder not only contains Pawno but also the Pawn code compiler (pawncc.exe).

If you store your Pawn compiler elsewhere, just replace the entire `command` setting with the full path to your compiler.

Also, if you want to disable debug symbols (you won't be able to use crashdetect) just remove `-d3` from `"args": ["${relativeFile}", "-;+", "-(+", "-d3"],`.

`problemMatcher` is the part that allows recognising the Pawn compiler output and presenting it in the `problems` panel of the editor. This doesn't work well with external includes because the paths change from relative to absolute. [sampctl](http://sampctl.com) fortunately fixes this (and a lot of other annoying things).

## Features

Currently just syntax highlighting.

Once the [Pawn-Parser](https://github.com/Southclaws/pawn-parser) project reaches a workable state, this extension will feature more language features such as intellisense support, go-to-definition, view-all-references, etc...
