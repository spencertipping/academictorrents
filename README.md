# Academic Torrents processes
I maintain some public datasets for local use and mirror them to [Academic
Torrents](https://academictorrents.com). This repository contains all of the
source code for those processes. Everything is run through Docker, so you should
be able to reproduce everything here.

**WIP:** none of this will work yet.

## What you'll need to run this
A lot of disk space: you need about 2TB free to create the larger datasets.

Most datasets can be processed within 1GB of memory, but OpenStreetMap uses
closer to 100GB. It's possible to process it in much less by sorting the node
list first, but that would slow down the workflow considerably.

## What's here
- [The docker image that runs everything](docker)
- [The dataset runner script](./run)

## Specific datasets
- [Wikipedia full history](wikipedia_history)
