---
title: "Qt compilation problems after fresh installation on Ubuntu"
date: 2021-08-27
author_profile: true
classes: wide
header:
  teaser: "assets/images/blog/exomy.jpg"
categories:
  - Notes
tags:
  - qt
  - c++
---

I just made a fresh installation of Qt6 on Linux machine running Ubuntu. It was failing to build a default widget application with the error. From the error message it seemed to be some CMake error about not being able to find Qt libraries.

```bash
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets REQUIRED)

Found package configuration file: /home/xxx/Qt/6.0.4/gcc_64/lib/cmake/Qt6/Qt6Config.make but it set Qt6_FOUND to FALSE so package "Qt6" is considered to be NOT FOUND. Reason given by package: Failed to find Qt component "Widgets" config file at""
```

But the [solution][Forum] was to install some OpenGL libraries. Seems on Ubuntu installation of OpenGL is a requirement for running Qt. The problem went away after I installed `libgl1-mesa-dev` with the command

```
apt install libgl1-mesa-dev
```

[Forum]: https://forum.qt.io/topic/129346/widgets-component-is-not-recognized-in-cmakelist-file/2
