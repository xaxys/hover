# Hover - Run Flutter apps on the desktop with hot-reload

Hover is a simple build tool to create flutter desktop applications.

**Hover is brand new and under development, it should be considered alpha. Anything can break, please backup your data before using hover**

## Getting started

### Install

First install go, then install hover like this:

```bash
go get -u github.com/go-flutter-desktop/hover
```

Run the same command to update when a newer version becomes available.

Install these dependencies:

* You need to make sure you have dependencies of GLFW:
	* On macOS, you need Xcode or Command Line Tools for Xcode (`xcode-select --install`) for required headers and libraries.
	* On Ubuntu/Debian-like Linux distributions, you need `libgl1-mesa-dev xorg-dev` packages.
	* On CentOS/Fedora-like Linux distributions, you need `libX11-devel libXcursor-devel libXrandr-devel libXinerama-devel mesa-libGL-devel libXi-devel` packages.
	* See [here](http://www.glfw.org/docs/latest/compile.html#compile_deps) for full details.

### Init project

cd into a flutter project.

```bash
cd projects/simpleApplication
```

The first time you use hover for a project, you'll need to initialize the project for desktop. `hover init` requires a project path. This is usualy the path for your project on github or a self-hosted git service. _If you are unsure, just make something up, it can always be changed later._

```bash
hover init github.com/my-organization/simpleApplication
```

This creates the directory `desktop` and adds boilerplate files such as Go code and a default logo.

Optionally, you may add [plugins](https://github.com/go-flutter-desktop/plugins) to `desktop/cmd/options.go`

Optionally, change the logo in `desktop/assets/logo.png`, which is used as icon for the window.

Make sure you have a main_desktop.dart that contains the following code before `runApp(..)`:

```dart
debugDefaultTargetPlatformOverride = TargetPlatform.fuchsia;
```

### Run with manual hot-reload

To run the application and attach flutter for hot-reload support:

```bash
hover run --target lib/main_desktop.dart
```

The hot-reload is manual because you'll need to press 'r' in the terminal to hot-reload the application.

### Build standalone application

To create a standalone debug build run this command:

```bash
hover build --target lib/main_desktop.dart
```

The output will be in `desktop/build/outputs/linux` or windows or darwin depending on your OS. Hover does not yet support cross-compilation.

To start the binary: (replace `yourApplicationName` with your app name)

```bash
./desktop/build/outputs/linux/yourApplicationName
```

It's possible to zip the whole dir `desktop/build/outputs/linux` and ship it to a different machine.

There is no support for release binaries yet, only debug.

## Issues

Please report issues at the [go-flutter issue tracker](https://github.com/go-flutter-desktop/go-flutter/issues/).
