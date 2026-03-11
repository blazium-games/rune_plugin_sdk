# Build Your Own Nodes for RUNE

You know RUNE? The visual node editor where you drag boxes and connect wires? This SDK lets you build *new* boxes. You write C or C++, RUNE loads your plugin, and suddenly your nodes show up in the editor. No magic, just a bit of code and a lot of fun.

This is for junior devs, curious beginners, anyone who wants to try something dumb and advanced. C/C++ can feel intimidating but the examples do most of the heavy lifting. Copy one, tweak it, see what breaks. Thats how you learn.

## Get RUNE First

You need the editor before any of this makes sense.

- [Rune Interface](https://bioblaze.blazium.games/rune-interface) - download and run it
- [Documentation](https://blazium-games.github.io/rune_docs/) - guides, API reference, node stuff

Grab the Windows build from itch, unzip it, point it at a cache and flows folder when it asks. Then come back here.

## What You Need

C or C++ (the examples use C++17). CMake 3.15 or newer. A compiler, whatever you got. MSVC, GCC, Clang, all fine. And RUNE installed, or runecli if youre doing headless stuff.

## Quick Start

Clone this repo. Cd into it. Build the math plugin:

```
cd examples/math_plugin
mkdir build
cd build
cmake ..
cmake --build .
```

You should get a `math_plugin.dll` (or .so on Linux, .dylib on Mac) in the `dist` folder. Copy that whole dist folder into wherever RUNE keeps its plugins. Launch RUNE and your Add, Multiply, Divide, Power nodes should be there under Math.

Easiest way to make your first plugin: copy the whole `math_plugin` folder, rename it to whatever. Change the plugin.json id and name. Then change one of the nodes. Like take Add and make it Subtract instead. Rebuild. Drop it in the plugins dir. Done.

## Node Types (In Plain English)

**Pure data** - Numbers and strings flow in and out. No run button, just data. The math plugin is all pure data.

**Trigger / Event** - Something happens. A timer fires, a button gets clicked. Your node wakes up and does its thing. Check out timer_plugin for this.

**Async** - The work takes time. Your node says "im not done yet" and finishes later. Delay in timer_plugin is async.

## Your First Plugin

Copy `examples/math_plugin` to something like `my_plugin`. Edit plugin.json, change the id to something unique (com.you.myplugin or whatever) and the name. Open the cpp file and add a simple node. A "Double" node: one float in, one float out, multiply by 2. Look at how Add is done and copy that structure. Register it in on_register. Build with cmake. Put the dll and plugin.json in RUNEs plugins directory. Fire up RUNE. Your node should be in the menu.

Oh and make sure the include path points at the SDK. In the math plugin CMakeLists the include is `../../include` cause its two levels down from the root. If you put your plugin somewhere else adjust that.

## Ideas to Try

Dumb stuff: a Hello World node that spits out a fixed string. A Random Compliment node. Something pointless. Seriously.

Advanced stuff: a node that reads a file and parses JSON. One that hits an HTTP API. A timer that fires every N seconds (timer_plugin already does this, rip it apart and change it). The config_plugin shows you how to do settings and menus. env_plugin does environment variables. Look at those when you want to go deeper.

## Example Plugins

- `math_plugin` - pure data, Add Multiply Divide Power
- `timer_plugin` - Timer Event and Delay, events and async
- `config_plugin` - settings, menus, JSON/CSV/INI parsing
- `env_plugin` - env vars, app settings

## Project Layout

```
rune_plugin_sdk/
  include/       - rune_plugin.h, plugin_api.h
  examples/      - four example plugins
  CMakeLists.txt
```

Headers are in include. Examples are in examples. Each example has its own CMakeLists and plugin.json.

## Go Build Something Weird

Break things. Ask questions. The examples are there to copy and twist. If something doesnt work, check the docs. If the docs dont help, thats fine too. Try a node that does something pointless. Thats how you learn.

[Rune Interface](https://bioblaze.blazium.games/rune-interface) | [Documentation](https://blazium-games.github.io/rune_docs/)
