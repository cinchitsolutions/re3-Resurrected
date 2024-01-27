# Intro

In this repository you'll find the fully reversed source code for GTA III & GTA VC.

This is all in an effort to resurrect the original project. This ONLY the PC verison. The Switch, WiiU, & PSVita versions will not be uploaded. 
My hope is to create a fully functional, moddable, and open version of the original repository that can be enjoyed for years to come. 

It has been tested and works on Windows, Linux, MacOS and FreeBSD, on x86, amd64, arm and arm64.\
Rendering is handled either by original RenderWare (D3D8)
or the reimplementation [librw](https://github.com/aap/librw) (D3D9, OpenGL 2.1 or above, OpenGL ES 2.0 or above).\
Audio is done with MSS (using dlls from original GTA) or OpenAL.

## Installation

- re3 requires PC game assets to work, so you **must** own a copy of the Original GTA 3 not the Definitive Editions.
- For now you must build this package from source. I will work on getting builds uploaded for ease of use. 
- Extract the downloaded zip over your GTA 3 directory and run re3. The zip includes the binary, updated and additional gamefiles and in case of OpenAL the required dlls.

## Screenshots

![re3 2021-02-11 22-57-03-23](https://user-images.githubusercontent.com/1521437/107704085-fbdabd00-6cbc-11eb-8406-8951a80ccb16.png)
![re3 2021-02-11 22-43-44-98](https://user-images.githubusercontent.com/1521437/107703339-cbdeea00-6cbb-11eb-8f0b-07daa105d470.png)
![re3 2021-02-11 22-46-33-76](https://user-images.githubusercontent.com/1521437/107703343-cd101700-6cbb-11eb-9ccd-012cb90524b7.png)
![re3 2021-02-11 22-50-29-54](https://user-images.githubusercontent.com/1521437/107703348-d00b0780-6cbb-11eb-8afd-054249c2b95e.png)

## Improvements

We have implemented a number of changes and improvements to the original game.
They can be configured in `core/config.h`.
Some of them can be toggled at runtime, some cannot.

* Fixed a lot of smaller and bigger bugs
* User files (saves and settings) stored in GTA root directory
* Settings stored in re3.ini file instead of gta3.set
* Debug menu to do and change various things (Ctrl-M to open)
* Debug camera (Ctrl-B to toggle)
* Rotatable camera
* XInput controller support (Windows)
* No loading screens between islands ("map memory usage" in menu)
* Skinned ped support (models from Xbox or Mobile)
* Rendering
  * Widescreen support (properly scaled HUD, Menu and FOV)
  * PS2 MatFX (vehicle reflections)
  * PS2 alpha test (better rendering of transparency)
  * PS2 particles
  * Xbox vehicle rendering
  * Xbox world lightmap rendering (needs Xbox map)
  * Xbox ped rim light
  * Xbox screen rain droplets
  * More customizable colourfilter
* Menu
  * Map
  * More options
  * Controller configuration menu
  * ...
* Can load DFFs and TXDs from other platforms, possibly with a performance penalty
* ...

## To-Do

The following things would be nice to have/do:

* Fix physics for high FPS
* Reverse remaining unused/debug functions
* Create custom ModMenu / Trainer with full linux support.
* 

## Modding

Asset modifications (models, texture, handling, script, ...) should work the same way as with original GTA for the most part.

CLEO scripts work with [CLEO Redux](https://github.com/cleolibrary/CLEO-Redux).

Mods that make changes to the code (dll/asi, limit adjusters) will *not* work.
Some things these mods do are already implemented in re3 (much of SkyGFX, GInput, SilentPatch, Widescreen fix),
others can easily be achieved (increasing limis, see `config.h`),
others will simply have to be rewritten and integrated into the code directly.
Sorry for the inconvenience.

## Building from Source  

When using premake, you may want to point GTA_III_RE_DIR environment variable to GTA3 root folder if you want the executable to be moved there via post-build script.

Clone the repository with `git clone --recursive https://github.com/GTA3D.git`. Then `cd re3-master` into the cloned repository.

Microsoft recently discontinued its downloads of the DX9 SDK. You can download an archived version here: https://archive.org/details/dxsdk_jun10

**If you choose OpenAL on Windows** You must read [Running OpenAL build on Windows](https://github.com/GTAmodding/re3/wiki/Running-OpenAL-build-on-Windows).
</details>

> :information_source: premake has an `--with-lto` option if you want the project to be compiled with Link Time Optimization.

> :information_source: There are various settings in [config.h](https://github.com/GTAmodding/re3/tree/master/src/core/config.h), you may want to take a look there.

> :information_source: re3 uses completely homebrew RenderWare-replacement rendering engine; [librw](https://github.com/aap/librw/). librw comes as submodule of re3, but you also can use LIBRW enviorenment variable to specify path to your own librw.

If you feel the need, you can also use CodeWarrior 7 to compile re3 using the supplied codewarrior/re3.mcp project - this requires the original RW33 libraries, and the DX8 SDK. The build is unstable compared to the MSVC builds though, and is mostly meant to serve as a reference.

## Contributing

We accept only these kinds of PRs;

- A new feature that exists in at least one of the GTAs (if it wasn't in III/VC then it doesn't have to be decompilation)  
- Game, UI or UX bug fixes (if it's a fix to original code, it should be behind FIX_BUGS)
- Platform-specific and/or unused code that's not been reversed yet
- Makes reversed code more understandable/accurate, as in "which code would produce this assembly".
- A new cross-platform skeleton/compatibility layer, or improvements to them
- Translation fixes, for languages original game supported
- Code that increase maintainability  

## History of the re3 project.

re3 was started sometime in the spring of 2018,
initially as a way to test reversed collision and physics code
inside the game.
This was done by replacing single functions of the game
with their reversed counterparts using a dll.

After a bit of work the project lay dormant for about a year
and was picked up again and pushed to github in May 2019.
At the time I (aap) had reversed around 10k lines of code and estimated
the final game to have around 200-250k.
Others quickly joined the effort (Fire_Head, shfil, erorcun and Nick007J
in time order, and Serge a bit later) and we made very quick progress
throughout the summer of 2019
after which the pace slowed down a bit.

Due to everyone staying home during the start of the Corona pandemic
everybody had a lot of time to work on re3 again and
we finally got a standalone exe in April 2020 (around 180k lines by then).

After the initial excitement and fixing and polishing the code further,
reVC was started in early May 2020 by starting from re3 code,
not by starting from scratch replacing functions with a dll.
After a few months of mostly steady progress we considered reVC
finished in December.

re3 was removed from github along with all of the alternate versions. 
My intention is to attempt and finsh what was started via "Clean Room" reverse engineering. 
I will not be using any decompiled code. Only building new items and resources from scratch.

If you would like to participate in the project you can reach me at mizfitxtm@gmail.com


## License

We don't feel like we're in a position to give this code a license.\
The code should only be used for educational, documentation and modding purposes.\
We do not encourage piracy or commercial use.\
Please keep derivate work open source and give proper credit.

## DISCLAIMER

All credit for this goes to the original individuals who started this project, this is no attempt to "steal" their work. 
Only trying to bring it back in the most ethical way, Hopefully Take Two will see that we want whats best for the preservation of video games. 
I do not claim to have written any of this code. I have made tweaks to the underlying code but nothing that will be too noticable or game breaking. 

I look forward to the future of this project and hope you enjoy what functionality we currently have. 
