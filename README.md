# SourceLogger

This is a small program written in Go which redirects
the output of the `srcds_linux` executable to stdout.

It can be used to fix for the following issue
> stdin and stdout no longer works for linux garry's mod srcds server 

For more insights head over to the discussion at 
[garraysmod-isse#2343](https://github.com/Facepunch/garrysmod-issues/issues/2343#issue-123386501).

## How to use

1. Download the latest release from GitHub
2. Put the file `source_logger` into the same directory as `srcds_linux`
2. Replace in your start script the call of `srcds_linux` or `srcds_run` with `source_logger`.

An example start script before:
````sh
#!/bin/bash
./srcds_run -maxplayers 16 +gamemode terrortown +map ttt_waterworld
````

A start script using SourceLogger
````sh
#!/bin/bash
./source_logger -maxplayers 16 +gamemode terrortown +map ttt_waterworld
````

All arguments to `source_logger` will be forwarded to `srcds_linux`, so you can just keep your old arguments.

#### Drawbacks

There is a small drawbacks while using this software: 
You can't use the _auto update_ feature of the `srcds_run` script, 
because the `srcds_linux` executable is called directly from the SourceLogger.

## How does it work?
This program uses [kr/pty](https://github.com/kr/pty) to create a pseudo console and capture its output.