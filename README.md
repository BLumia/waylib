# waylib

## Introduction

waylib is a Wayland compositor development library, based on [wlroots](https://gitlab.freedesktop.org/wlroots/wlroots), provides a Qt-style development interface. It is designed to be deeply integrated with QtQuick, taking advantage of QtQuick's Scene Graphics model to simplify the complexity of window management. In waylib, each Output is a QQuickWindow and each Surface is a QQuickItem, allowing it to be mixed with QtQuick's graphics components and supporting QRHI for OpenGL and Vulkan compatibility in a single piece of code.

Creating a Wayland compositor using waylib can be simple and efficient, which, on top of wlroots, provides:

* QtQuick-based rendering model
* Qt event model support
* Session management system (under development)
* Client/window group policies (under development)
* Window motion system (under development)
* Window management abstraction (under development)

Based on the above features, compositor developers need only focus on the business requirements of window management and can develop window compositors as if they were implementing a regular application.

## Features

* Support switch different display backend: DRM, Wayland, X11
* Support custom input backend, by default it uses libinput
* Support for rendering cursors in both hardware and software
* Support for X Window cursor file format and theme
* Support for running in environments without dri devices
* Coexistence with Qt platform plug-in system
* Provides QML components

## Building

Step 1: Compile and install [wlroots](https://gitlab.freedesktop.org/wlroots/wlroots#building)


Step 2: Install dependencies

Debian
````
# apt install pkg-config qtbase5-private-dev qtbase5-dev-tools qtdeclarative5-private-dev qtquickcontrols2-5-dev wayland-protocols libpixman-1-dev
````

Archlinux

````
# pacman -Syu --noconfirm qt cmake pkgconfig wlroots pixman wayland-protocols ninja
````

Step 3: Execute the following commands

```bash
cmake -B build
cmake --build build
```

## How to Contribute

This project assumes that you already have experience with `Qt` and `wlroots` libraries. In order to better integrate with Qt and wlroots, waylib adheres to Qt's guidelines in terms of interface style, wlroots' modular design philosophy with regards to the underlying design, and Qt's wrapping + layering design for the upper layers that are not directly related to wlroots.

You are free to contribute as much code as you want to this project, provided that you follow the waylib design philosophy and the following types of requirements.

### Code Style

* When modifying existing code, the current code style should be respected.
* New code: the part that is closely related to wlroots should follow the code style of wlroots, such as when using `WSignalConnector` to link `wl_signal`, underscore naming convention should be used for the corresponding slot function; other parts should follow the code style of Qt (https://wiki.qt.io/Qt_Coding_Style this link is for reference only. The actual Qt source code shall prevail)
* There is no absolute right or wrong code style, please consider the big picture, and do not rigidly stick to the small details

### Code Architecture Guidelines

* The code should be simple and easy to understand.
* Add comments to key nodes whether you change or add new code
* Security > Compatibility > Extensibility >= Performance

### Contribution Guideline

* Contribution steps.
    1. First login to your Github account and fork the project
    2. Pull the forked project locally using `git clone`.
    3. Push the new commit to your project using `git push`.
    4. commit your code to the upstream project on Github using the Pull Requese feature.
* commit message specification: align with Qt project, use English. Be sure to describe exactly what the commit "does" and "why it was made"
* A commit only does one thing, and the smaller the code changes, the easier it is to accept the commit. For larger code changes, try to split the commit into multiple commits (satisfying the git commit principle as a prerequisite)
* Please do your own testing and code review before committing the code, and submit the PR after confirming that the code is working correctly

## Roadmap

* Support of vulkan
* Support Hardware Plane
* Support for virtual devices (remote screen projection, mouse, keyboard multi-device sharing)
* Support multi-platform integration
* Support high refresh rate (120Hz)
* Support variable screen refresh rate
