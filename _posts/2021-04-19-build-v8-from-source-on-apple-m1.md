---
layout: post
title: Build v8 from source on Apple M1
categories: v8
---


Follow up [Build v8 from source on Ubuntu 20.04]({{ site.baseurl }}{% link _posts/2021-02-20-build-v8-from-source.md %})). Today we're gonna build v8 source on an Apple M1 chip MacOS.

# Required
- bash shell
- git
- [Xcode](https://apps.apple.com/vn/app/xcode/id497799835?mt=12)
- python2

I  set up the V8 source code inside `~/Code/` folder and use it throughout this article. You can change it to your desired folder.

# Prepare the tools
- First we need to get the depot tools bundle from google. It's a package of scripts, to automate tasks to manage repositories http://www.chromium.org/developers/how-tos/install-depot-tools  
`git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git`  
- `export PATH=~/Code/depot_tools:$PATH`  
- `fetch v8`
- Download `gn` and extract it into `~/Code/` https://chrome-infra-packages.appspot.com/dl/gn/gn/linux-amd64/+/latest -o gn.zip
- Add it to path the same way as depot_tools then try `gn` command.

# Install dependencies
- `cd v8`
- `export PATH=~/Code/v8/tools/dev:$PATH`. This will help run build commands quicker.
- Try `gm.py arm64.release.d8` to see if it start building. Note: your python must be version `2.x.x`. If not, try switch python version using pyenv or any python version management tool. Otherwise you can run `python2 tools/dev/gm.py arm64.release.d8` instead.
- After a couple minutes, check the `out/arm64.release` folder to see the result.

# Play with V8
After building the source code, you will be able to use `d8`. V8's own developer shell. 
- `$ ./out/arm64.release/d8 `  
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
