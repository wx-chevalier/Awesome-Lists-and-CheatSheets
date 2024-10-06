# FFmpeg

- [2015-An ffmpeg and SDL Tutorial](http://dranger.com/ffmpeg/): This tutorial is meant for people with a decent programming background. At the very least you should know C and have some idea about concepts like queues, mutexes, and so on. You should know some basics about multimedia; things like waveforms and such, but you don't need to know a lot, as I explain a lot of those concepts in this tutorial.

- [2022~FFmpeg: The Ultimate Guide](https://img.ly/blog/ultimate-guide-to-ffmpeg/): This guide covers the ins and outs of FFmpeg starting with fundamental concepts and moving to media transcoding and video and audio processing providing practical examples along the way.

- [2023~ffmprovisr #Series#](https://amiaopensource.github.io/ffmprovisr/): This page does not have search functionality, but you can open all recipes (second option in the sidebar) and use your browser's search tool (often ctrl+f or cmd+f) to perform a keyword search through all recipes.

# OpenSource

- [2019~ffmpeg.wasm ![code](https://ng-tech.icu/assets/code.svg)](https://ffmpegwasm.github.io/): ffmpeg.wasm is a pure WebAssembly/JavaScript port of FFmpeg. It enables video & audio record, convert and stream right inside browsers.

- [Learn FFmpeg libav the Hard Way](https://parg.co/UkX): I was looking for a tutorial/book that would teach me how to start to use FFmpeg as a library (a.k.a. libav) and then I found the "How to write a video player in less than 1k lines" tutorial. Unfortunately it was deprecated, so I decided to write this one.

- [2015-How to Write a Video Player in Less Than 1000 Lines](http://dranger.com/ffmpeg/ffmpeg.html): There is a sample program that comes with ffmpeg called ffplay. It is a simple C program that implements a complete video player using ffmpeg.

- [2024~steelbrain/ffmpeg-over-ip ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/steelbrain/ffmpeg-over-ip)](https://github.com/steelbrain/ffmpeg-over-ip): Connect to remote ffmpeg servers. Are you tired of unsuccessfully trying to pass your GPU through to a docker container running in a VM? So was I! ffmpeg-over-ip allows you to run an ffmpeg server on a machine with access to a GPU (Linux, Windows, or Mac) and connect to it from a remote machine. The only thing you need is Node.js installed and a shared filesystem (could be NFS, SMB, etc.) between the two machines.
