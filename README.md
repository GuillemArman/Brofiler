# Brofiler
A research project about Brofiler implementation in C++.

What are profilers? Why do we use them?

these are some questions that will be answered on my research about Brofiler.

### Profilers

Profiling is a form of dynamic program analysis that measures, for example, the space (memory) or time complexity of a program, the usage of particular instructions, or the frequency and duration of function calls. It is used for optimization.

Program analysis tools are extremely important for understanding program behavior. Computer architects need such tools to evaluate how well programs will perform on new architectures. Software writers need tools to analyze their programs and identify critical sections of code. Compiler writers often use such tools to find out how well their instruction scheduling or branch prediction algorithm is performing.

On this wiki I am going to focus on the Brofiler profiler.

### Brofiler

Brofiler is an external profiling tool developed by Vadim Slyusarev. The Author describes the tool as a "Super Lightweight C++ Profiler for Games". While other profilers often can come with a huge overhead, Brofiler focuses on finding the most expensive functions.

![](http://brofiler.com/images/screenshots/Screen2.png)


**On this chapter you can learn how to implement Brofiler on your engine following the next steps:**

### Step 1: Download
Download and unzip archive with precompiled libraries:
* Brofiler.exe (GUI for visualizing results)
* Brofiler.h (Header to include)
* ProfilerCore64.lib (Library to link)
* ProfilerCore64.dll (DLL with implementation)
* EasyHook64.dll ([EasyHook](http://easyhook.codeplex.com/))
* ProfilerTest64.exe (Small console application to test profiler)

([Download]https://github.com/bombomby/brofiler/releases)

### Step 2: Integration
* Add recently unpacked directory to **Project Properties -> C/C++ -> Additional Include Directories**
* Add **ProfilerCore.lib** to **Project Properties -> Linker -> Input -> Additional Dependencies**
* Find Main Loop of your Game and insert **BROFILER_FRAME** macros:

```c++
#include "Brofiler.h"

while(true)
{ BROFILER_FRAME("YourThreadName")
  ...
}
```
* Copy **ProfilerCore64.dll** and **EasyHook64.dll** to your working directory

### Step 3: First Launch
Launch your Game.  
Launch Brofiler.exe.  
Click Start Button ![](http://brofiler.com/tutorial/start.jpg).  
![](http://brofiler.com/tutorial/progress.png)  
When you are ready click Stop Button ![](http://brofiler.com/tutorial/stop.jpg).  
If your see a picture similar to this one - everything is OK, move to the next step.
![](http://brofiler.com/tutorial/first_run.png)  

### Step 4: Instrumentation Mode
Add some profiling counters to your code.
```c++
#include "Brofiler.h"

//Just add BROFILE macros at the beginning of a function
void Engine::UpdateInput()
{ BROFILE

}
```

Add some profiling categories to your code (colorized counters).
```c++
#include "Brofiler.h"

//There is a lot of predefined standard colors, more than 100.
void Engine::UpdateLogic()
{ BROFILER_CATEGORY( "UpdateLogic", Profiler::Color::Orchid )
  
}
```
![](http://brofiler.com/tutorial/counters.png)

### Step 5: Sampling Mode
Check suspect functions in the table.  
![](http://brofiler.com/tutorial/sampling_checked.png)
From now these functions are marked for sampling.  
All the code inside the scope of these functions will be sampled during next run.  
Click Start Button to start new profiling run, press Stop Button to get results.  
Click ![](http://brofiler.com/tutorial/clear_sampling.png) to clear all sampling scopes.![](http://brofiler.com/tutorial/sampling.png)

### Step 6: Hooking Mode
Open any Sampling Frame. Click a checkbox in the table with sampling results to inject profiler counter inside this function.  
1[](http://brofiler.com/tutorial/hooking_checked.png)
Get another profining run.  
Click ![](http://brofiler.com/tutorial/hooking_icon.png) to remove all injected counters.  
![](http://brofiler.com/tutorial/hooking.png)

### Step 7: Source View
Double click on any row in the table will open Source View window.
![](http://brofiler.com/tutorial/source2.png)

### Step 8: Save and Load
Click ![](http://brofiler.com/tutorial/save_icon.png) to save *.prof file with active session.  
Drag and Drop any *.prof file on the timeline to load it.


https://github.com/GuillemArman/Brofiler/wiki/Tutorial


## Brofiler Overview

The threads panel gives a general overview of what is going on in the main thread. Labels have been added as so called Regions inside CRYENGINE. 
These are high-level labels or very important labels and are always collected:
* Light blue = busy time
* Yellow = waiting time

![](http://docs.cryengine.com/download/attachments/24283922/image2016-3-11%2015%3A22%3A51.png?version=1&modificationDate=1457706171000&api=v2)


Below the threads panel you get a listed overview of the Regions which are sorted by the lifetime of the label:

![](http://docs.cryengine.com/download/attachments/24283922/image2016-3-11%2015%3A28%3A31.png?version=1&modificationDate=1457706511000&api=v2)

With this analyisis you can check which function takes more time and look for the problem in the code. 

### Drawbacks
- If Brofiler is used in an extern computer you will not be able to use the Sampling Mode. 
- If the game crashes, Brofiler stops recording.


## TODO'S

Download the zip ([here]https://github.com/GuillemArman/Brofiler/blob/master/Brofiler_research_exercise.zip)

- TODO 1:Integrate Brofiler into new directories
 Hint: Don't forget to add all the files you need into Game directory
 
 - TODO 2: include Brofiler.h and the library
 
- TODO 3: Find Main Loop of your Game and insert BROFILER_FRAME macros
 
- TODO4: Include a Brofiler macro to see how Brofiler works
 
- TODO5: Implement Brofiler on your project and look for the slowlest function
