---
layout: post
title:  "Creating C4 Software Architecture diagrams using VSCode and PlantUML"
date:   2020-01-14 17:28:00 +0100
categories: 
---

# Introduction

This post introduces a way to create and maintain software architecture diagrams, based on the C4 Model, using PlantUML. If you are unfamiliar with the C4 modelling language, feel free to check out [my introduction](2020/01/06/an-introduction-to-the-c4-modelling-language.html).

In short, you will be able to turn the contents of the following `.puml` file into the C4 diagram below it. It will do this both as a preview as you're writing it, and as a `.png` file on disk after each time you save, using Visual Studio Code.

<script src="https://gist.github.com/nielsabels/4b7dca1c17bdfeb5f10da58e52c67954.js"></script>

![c4-system-context](/assets/img/2020-01-14/c4-system-context.png)

# How-to guide

## Clone the repository

Clone the GitHub repository and open it with VSCode.

```console
git clone https://github.com/nielsabels/c4-diagrams-plantuml-starter
cd c4-diagrams-plantuml-starter
code .
```

## Install extensions

The following popup should appear:

![extensions_installer_popup](/assets/img/2020-01-14/extensions_installer_popup.png)

Click "`Install All`" to install the following recommendations.

![extensions_workspace_recommendations](/assets/img/2020-01-14/extensions_workspace_recommendations.png)

The `PlantUML` extension is used to preview images in VSCode later on and provides syntax-highlighting. `Trigger Task on Save` is used to export a `.png` diagram upon change of any PlantUML markup file.

## Start PlantUML server

Next up is starting the PlantUML server which will be used by VSCode to translate the PlantUML markup to images (`.png`).

### Docker

Docker is required to host the PlantUML server. Click here to read how to install it on [Windows](https://docs.docker.com/docker-for-windows/install/), [Mac](https://docs.docker.com/docker-for-mac/install/) or [Linux](https://docs.docker.com/compose/install/). Make to include Docker Compose as an installation option, we will be using it to start/stop the PlantUML server with a little bit more ease.

### Starting the server

Start the PlantUML server using the (`.sh`, `.ps1`, `.cmd`) scripts in the `/scripts` directory.

```console
cd scripts
./start_server.sh

Creating network "c4-diagrams-plantuml-starter_default" with the default driver
Creating c4-diagrams-plantuml-starter_plantuml_1 ... done
```

## Wrapping up

At this stage, you should be ready to create C4 diagrams using VSCode. 

- Open the `c4-diagrams-plantuml-starter` directory using VSCode.
- Navigate to a PlantUML file (e.g. `diagrams/C4 System Context - Internet Banking System.puml`).
- Continue by pressing `ctrl+p` to open the action panel and enter a `>` character followed by a space character to list the actions.
- Find the action `PlantUML: Preview Current Diagram` to get a panel next to your source file. 

![vscode_preview](/assets/img/2020-01-14/vscode-preview.gif)

# Credits

