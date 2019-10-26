# Resurrect 0xbench

This repo was cloned from 0xbench project, which was integrated Android benchmark suite by 0xlab. 
Howerver, it's died after oct 27, 2011. I recently discovered this excellent project and decided to revive it.
Now, the original 0xbench app can already run on my phone, so I'll release this project again, and I hope
it will be useful.

## Project info

0xlab integrated a series of benchmark for Android system into
the comprehensice benchmark suite, [0xbench](https://code.google.com/archive/p/0xbench/).

**Key Feature**

- Full open source. License terms: Apache Software License(primary), CDDL(partial)
- Comprehensive benchmarking: from system call(bionic) to Android frameworks
- Community development process: accept open source contibutions for benchmark iterms and reference results

**Coverage**

- C library and system call
- OpenGL|ES
- 2D canvas
- Garbage collection in Dalvik/ART
- JavaScript engine

**Benchmark**

[Current included benchmarks](https://code.google.com/archive/p/0xbench/wikis/Benchmarks.wiki)

Arithmetic
- Linpack
- Scimark

Web
- SunSpider

2D
- Canvas Redraw
- Draw Circle
- Draw Rect
- Draw Circle2
- Draw Arc
- Draw Text
- Draw Image

3D
- GL Cube
- GL Teapot
- NEHE Lesson08
- NEHE Lesson16

Dalvik/ART
- Garbage Collection

Native
- LibMicro
- BYTE UnixBench


## Building APK(SDK)

An APK image contains all built-in Java-based benchmarks and a interface to the native C based benchmarks, but not the 
C binaries itself.

**Using Eclipse**

1. Download and install Android SDK and Eclipse IDE.
2. In Eclipse, click File -> New -> Android Project.
3. In the new project dialog, select Create project from existing source , select the path to 0xbench.
4. Click Finish to create project in Eclipse.

**Building and Deploying Standalone Binaries(NDK)**

1. Download and install both Android SDK and Android NDK.
2. In the project directory (0xbench), build binaries with the command: /path/to/ndk/ndk-build
3. The binaries can be found under /path/to/0xbench/libs/armeabi/bench\_\*. Use root permission to mount /system with rw permission, and use adb to deploy: adb push /path/to/0xbench/libs/armeabi/bench\_\* /system/bin/

## What I Do

So far, everything seems to be trivial. In fact, there are still a few words I want to explain to you, otherwise you may feel confused.

1. The CHAGELOG in this project says, "Package name changed from org.zeroxlab.benchmark to org.zeroxlab.zeroxbenchmark", but I don't know why the autor do this!
When I built it in my Ecplise, it failed. Finally, I fixed this by changing the pakeage name "org.zerolab.zeroxbenchmakr" to "org.zerolab.benchmark".

2. Compiling the native code in Eclipse requires creating a new NDK builder: 
Right click on the project name -> properties -> Builders -> New -> Program and fill in the tab.

 Main->Name: NDK_Builder

 Main->Location: /path/to/ndk/ndk-build

 Main->Working Directory: ${your project path}

 Build Options -> Specify Resources: select /path/to/0xbench/jni/

 You also need to selcet some checkbox in there, if you don't know how to do this, typing on Google.

3. If compile native code failed arround "valloc" function, replace "valloc" to "memalign".

4. When you deploying standlone binaries from "/path/to/0xbench/libs/armeabi/bench\_\*" to "/system/bin by using "adb push" failed,
you may have not root permission and "/system" is read-only permission. Now, you just run and config your AVD emulator as follow:

 ```
 $ cd /path/to/sdk/tools
 $ emulator -avd your_avd_name -writable-system
 $ adb root
 $ adb remount
 ```

5. When you want to test native benchmark in 0xbench app, do the above step first.

That is all above, if you have any question about 0xbench, issue me.

## What's next

Next, I will refactor this project on Android Studio, add and update some benchmarks in 0xbench.

**TODO**
1. Refactor this project on Android Studio to fit higher Android system version.
2. Update Linpack and Scimark2 java benchmark.
3. Add SPECjvm2008 in.
4. Review native benchmark in 0xbench.

