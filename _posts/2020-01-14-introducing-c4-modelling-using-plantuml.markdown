---
layout: post
title:  "Creating C4 Software Architecture diagrams using VSCode and PlantUML"
date:   2020-01-14 17:28:00 +0100
categories: 
---

# Introduction

This post introduces a way to create and maintain software architecture diagrams, based on the C4 Model, using PlantUML. If you are unfamiliar with the C4 modelling language, feel free to check out [my introduction](2020/01/06/an-introduction-to-the-c4-modelling-language.html).

The instructions in this post will make you able to turn a `.puml` (PlantUML markup file) into a C4 diagram. This diagram will be available as a live preview while you edit the `.puml` file in Visual Studio Code. It will also appear as a `.png` image file on disk, each time after you save the `.puml` file.

The following is an example of an architectural diagram in the PlantUML syntax.

<script src="https://gist.github.com/nielsabels/4b7dca1c17bdfeb5f10da58e52c67954.js"></script>

The above definition can be visually represented as the following image.

![c4-system-context](/assets/img/2020-01-14/c4-system-context.png)

Once you're done following along with this blog post, the VSCode editor will render C4 diagrams based on changes to the PlantUML file, like below.

![vscode_preview](/assets/img/2020-01-14/vscode-preview.gif)

## How It Works

It's a GitHub repository which is meant to be used with VSCode. It has been pre-configured to recommend extensions and has sensible defaults to enable live-previewing and auto-exporting (upon save) of C4 diagrams.

The rendering of images is off-loaded to a rendering engine (PlantUML Server) and is not done within VSCode. This means that it needs to be started next to VSCode in order for the previewing/exporting functionality to work. In the repository you will find a `docker-compose` file which you can use to spin up the required dependencies. The configuration to point VSCode to the rendering engine _[should](https://github.com/nielsabels/c4-diagrams-plantuml-starter/blob/86651da4732a9aa593c4c74d96736e541c24fadb/.vscode/settings.json#L5) just [work](https://github.com/nielsabels/c4-diagrams-plantuml-starter/blob/86651da4732a9aa593c4c74d96736e541c24fadb/docker-compose.yml#L6)_.

# Grabbing the GitHub repository

Clone the GitHub repository and open it with [VSCode](www.vscode.com).

```console
git clone https://github.com/nielsabels/c4-diagrams-plantuml-starter
cd c4-diagrams-plantuml-starter
code .
```

Alternatively, download the latest version using your browser [here](https://github.com/nielsabels/c4-diagrams-plantuml-starter/archive/master.zip) and open the unzipped directory using VSCode.

## Installing the Recommended Extensions 

The following popup should appear:

![extensions_installer_popup](/assets/img/2020-01-14/extensions_installer_popup.png)

Click "`Install All`" to install the following recommendations.

![extensions_workspace_recommendations](/assets/img/2020-01-14/extensions_workspace_recommendations.png)

The `PlantUML` extension is what allows us to preview images in VSCode and provides syntax-highlighting for `.puml` files. `Trigger Task on Save` is used to export a `.png` diagram upon change of any PlantUML markup file.

## Starting the PlantUML Server

This section contains information for starting a PlantUML server using Docker and Docker Compose to ease collaboration when working in a team. 

If you feel unfamiliar with this, please follow these alternative steps. [Follow this section](https://github.com/qjebbs/vscode-plantuml#requirements) to install Graphviz/PlantUML locally. And remove the line in the configuration file [marked here](https://github.com/nielsabels/c4-diagrams-plantuml-starter/blob/86651da4732a9aa593c4c74d96736e541c24fadb/.vscode/settings.json#L5). Skip to the [Wrapping Up](#wrapping-up).

### The Docker and Docker-Compose Route

Docker is required to host the PlantUML server. Click here to read how to install it on [Windows](https://docs.docker.com/docker-for-windows/install/), [Mac](https://docs.docker.com/docker-for-mac/install/) or [Linux](https://docs.docker.com/compose/install/). Include Docker Compose as an installation option, we will be using it to start/stop the PlantUML server with a little bit more ease.

### Starting the server

Start the PlantUML server using the (`.sh`, `.ps1`, `.cmd`) scripts in the `/scripts` directory. Use `start_server.X` and `stop_server.X` when respectively starting/stopping the rendering engine, or just leave it running after running `start_server.X`.

```console
cd scripts
./start_server.sh

Creating network "c4-diagrams-plantuml-starter_default" with the default driver
Creating c4-diagrams-plantuml-starter_plantuml_1 ... done
```

## Wrapping up

At this stage, you should have everything installed and ready to create C4 diagrams using VSCode. 

If you haven't already, open the `c4-diagrams-plantuml-starter` directory using VSCode. Navigate to a PlantUML file (e.g. `diagrams/C4 System Context - Internet Banking System.puml`). Continue by pressing `ctrl+p` to open the action panel and enter a `>` character followed by a space character to list the actions. Find the action `PlantUML: Preview Current Diagram` to get a panel next to your source file. 

![vscode_preview](/assets/img/2020-01-14/vscode-plantuml-command.png)

That's it. Have fun making C4 diagrams!

# Credits

- [Trigger Task on Save](https://github.com/Gruntfuggly/triggertaskonsave) - A Visual Studio Code extension to trigger tasks when saving files.
- [vscode-plantuml](https://github.com/qjebbs/vscode-plantuml) - Rich PlantUML support for Visual Studio Code.
- [Simon Brown](https://simonbrown.je/) - Creator of the C4 Model for Software Architecture.
- [PlantUML](https://plantuml.com/) - Easily create beautiful UML Diagrams from simple textual description.
- [VSCode](www.vscode.com) - Visual Studio Code is a source-code editor developed by Microsoft for Windows, Linux and macOS.
- [Docker](www.docker.com) - A set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.
