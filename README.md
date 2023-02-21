<!-- Compile to html with https://markdowntohtml.com/ -->

# Napoleon Total War: Intel 12th-gen Patch Tutorial
*A guide on how to patch Napoleon Total War to run on Intel 12th & 13th gen processors, such as the i9-12900k which NTW has been known not to be able to boot on up until now due to DRM issues.*


We will be:
1. Installing Ghidra - a reverse engineering toolsuite
2. Using it to modify the Napoleon.exe executable, namely replace all CPUID 0f a2 instructions with XOR ECX, ECX or 33 c9.
3. Play the game on our Intel 12th-gen device. In my case Im testing on an i9-12900k desktop processor.

### Binary download links

https://github.com/ItsCubeTime/Napoleon-Total-War-Intel-12th-gen-patch/releases
https://terabox.com/s/1gXOUndbPoj1_MHRcUOf5Yg

*As an alternative to creating the patch yourself using Ghidra, you can also just install my pre-patched executable. To use it, you simply locate Napoleon.exe in your Napoleon Total War install directory & replace it with the patched executable linked above (and rename it accordingly), aftet that the patch is complete & you should be able to fire up the game like normal (except, this time it wont shut itself down immediately).*

*On most systems, the executable will be located at `C:\Program Files (x86)\Steam\steamapps\common\Napoleon Total War\Napoleon.exe`*

### Video guide

https://www.youtube.com/watch?v=-gUf6t6yDXo

### Text guide

1. Install Ghidra from: https://github.com/NationalSecurityAgency/ghidra/releases
2. Run ghidraRun.bat
3. Topbar > File > New Project.
4. Once you've created a new project, click the green dragon to open it up using the "CodeBrowser".
5. CodeBrowser > Topbar > File > Import. Select  `steamapps/Napoleon Total War/Napoleon.exe`.
6. Topbar > Search > Memory
7. Set Byte Order to Big Endian, Memory Block Types to All Blocks. "Search All" for `0f a2`.
8. Replace all "CPUID" instructions with `33 c9` by selecting them one by one in the Search Results window, going into the text editor view of your CodeBrowser main window, rightclicking the CPUID line & selecting `Patch Instruction`, then type in `XOR ECX, ECX` & select `33 c9` by left clicking on it in the dropdown. These instructions are known as `Assembly opcode`, see table: http://ref.x86asm.net/coder32.html.
8. Once all CPUID instructions (and only the CPUID instructions) have been replaced as described above, go to Topbar > File > Export Program, set the `Format` to `binary` and set a file path.
10. Now you have your patched binary! Navigate to the file path and replace your `steamapps/Napoleon Total War/Napoleon.exe` with your patched file. I recommend making a backup of the old file in case you accidentally modified something else in the process, same goes for your patched file in case Steam ever tries to revert your patch. :)


#### Fire up the game & enjoy your 12th gen CPU! Thanks for reading 💖

### Known issues

* Multiplayer appears to require that both players use the patch. See: https://imgur.com/a/eBRXG4p . Please open an issue on our Github page if you find a solution for this https://github.com/ItsCubeTime/Napoleon-Total-War-Intel-12th-gen-patch/issues

### Credits
* Redditor LogicalMaintenance35 *for discovering the patch  https://www.reddit.com/r/totalwar/comments/za16n4/comment/j899js4/?utm_source=share&utm_medium=web2x&context=3*
* Olliver A, *For writing this guide & recording linked video based on Logical's patch.*

### Links to this guide:
* https://forums.totalwar.com/discussion/328436/intel-12th-gen-patch-tested-running-with-no-performance-issues-on-intel-i9-12900k-w-ecores-enabled/
* https://github.com/ItsCubeTime/Napoleon-Total-War-Intel-12th-gen-patch
