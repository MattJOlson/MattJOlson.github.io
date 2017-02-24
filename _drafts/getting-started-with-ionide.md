---
layout: post
title: Getting Started With Ionide
---

# A Guide For Visual Studio Refugees

I'm getting a bit sick of Visual Studio for my F# needs. Maybe you are
too! As it happens, [Visual Studio Code](***link***) is coming along
nicely as a lightweight alternative, thanks to the [Ionide](***link***)
plugin. This post is a walkthrough of getting an alternative F#
development environment set up under Windows. (You should be able to
follow a similar workflow under Linux or MacOS.)

We'll be using the following tools: (XXX: Links)

* Visual Studio Code, an Electron-based editor not unlike Atom. (Ionide
  is also available for Atom, but I haven't tried it.)
* Ionide, a fantastically comprehensive F# plugin for VS Code
* Forge, a CLI project-management tool for F#
* Paket, a package manager built around F#
* FAKE, a build tool built in F#
* Expecto, a compositional testing framework for F#

Sounds like a lot, doesn't it? If you're on the Ionide train, it'll
probably turn out to be a feature rather than a bug. Rather than crawl
through endless mazes in VS to manage dependencies or build
configurations, you can learn a bit about FAKE, or a bit about Paket,
and know exactly where to apply that knowledge.

I'm going to assume that, if you're unhappy with Visual Studio, you
probably want to spend a bit more time on the command line or
thereabouts. If you're looking for an F# dev tool that's "the same, but
different" -- a single, big,  integrated piece of software -- you might
find _some_ of what you want here.

## 1. What you'll need to install

http://kcieslak.io/Working-with-F-Projects-In-VSCode

- install F# 4.0
- install MS build tools
- install VS Code
- install Ionide, Ionide/Paket, Ionide/FAKE plugins
- install Forge
- (install Vim package and FiraCode:
  https://github.com/tonsky/FiraCode/wiki/VS-Code-Instructions)

C-S-P F#: New Project
- uses Forge to create a new project structure

First attempt at C-S-P FAKE Build:
  1) Building
  c:\dev\fuckaround\console-test\console-test\console-test.fsproj failed
  with exitcode 1.   2) MSB3644: C:\Program Files
  (x86)\MSBuild\14.0\bin\Microsoft.Common.CurrentVersion.targets(1098,5):
  The reference assemblies for framework ".NETFramework,Version=v4.6.2"
  were not found. To resolve this, install the SDK or Targeting Pack for
  this framework version or retarget your application to a version of
  the framework for which you have the SDK or Targeting Pack installed.
  Note that assemblies will be resolved from the Global Assembly Cache
  (GAC) and will be used in place of reference assemblies. Therefore
  your assembly may not be correctly targeted for the framework you
  intend.---------------------------------------------------------------------

4.6.2 targeting pack or w/e not listed as installed
try installing:
  https://www.microsoft.com/en-us/download/details.aspx?id=53321
  -that worked

ctrl-F5 builds, yey

interesting, if you open in the top-level ctrl-F5 will build into
./build/ by default, not e.g. fsprojdir/bin/Debug/

C-S-P Paket: Add NuGet package | Newtonsoft.Json
How to add it as a reference tho, it's included in the .fsproj but
doesn't autocomplete
ah, not downloaded I guess? No, it's in ./packages/Newtonsoft.Json
Aha! Open foo.fsproj, from that buffer, CSP Paket Add Nuget Package (to
current project)
- That adds it to foo.fsproj and paket.dependencies, but build can't
  find it
