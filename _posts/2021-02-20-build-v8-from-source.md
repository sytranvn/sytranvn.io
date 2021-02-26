---
layout: post
title:  "Build v8 from source on Ubuntu 20.04"
categories: v8
tags: [v8,cpp]
---

Have you ever asked what does V8 do? Here's how to build a V8 of your own from source code. See what it can do and even have fun with it.

# Required
- bash shell
- git

I  set up the V8 source code inside `~/Code/` folder and use it throughout this article. You can change it to your desired folder.

# Prepare the tools
- First we need to get the depot tools bundle from google. It's a package of scripts, to automate tasks to manage repositories http://www.chromium.org/developers/how-tos/install-depot-tools  
`git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git`  
- `export PATH=~/Code/depot_tools:$PATH`  
- `fetch v8`
- Download `gn` from https://chrome-infra-packages.appspot.com/dl/gn/gn/linux-amd64/+/latest 
- Add it to path the same way as depot_tools then try `gn` command.

# Install dependencies
- `cd v8`
- Run magic script to install everything needed `./build/install-build-deps.sh` (you have to provide sudo password)
- `export PATH=~/Code/v8/tools/dev:$PATH`. This will help run build commands quicker.
- Try `gm.py x64.release` to see if it start building. Note: your python must be version `2.x.x`. If not, try switch python version using pyenv or any python version management tool. Otherwise you can run `python2 tools/dev/gm.py x64.release` instead.
- After a couple minutes, check the `out/x64.release` folder to see the result.

# Play with V8
After building the source code, you will be able to use `d8`. V8's own developer shell. 
- `$ ./out/x64.release/d8 `  
   `V8 version 9.0.0 (candidate)`
- Try writing some Javascripts, eg:  
```js
d8> console.log('Hello V8!')
Hello V8!
undefined
d8> for (let i = 0; i < 5; i++) console.log(i)
0
1
2
3
4
undefined
d8> 
``` 

# What's next?
You now have all the control over the engine. You can modify the source code, build and test it using `d8`.

Goodluck have fun!