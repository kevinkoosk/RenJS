+++
title = "File Structure"
date =  2018-05-16T14:41:12+02:00
weight = 5
pre = "<b>1.1 </b>"
+++

The quickstart is composed of a few files and folders, including the "executable" file index.html. Creating a game with RenJS means creating also a web page that runs said game. This allows you to ship your game to any platform that can run a web browser: Linux, Mac, Windows and even mobile devices, without needing to change your code. 

Let's take a look at these files:

* RenJS
* libs
* assets
* story
* index.html
* config.js

## Index

The index.html file is the web page where the game will be shown. The contents are minimal, the only thing we need to do here is to call the files that will load the game. Those files are:

* Phaser: The most important library of the engine, it takes care of the low level parts of the game like showing images, reproducing sound, etc.
* Config: The global configuration for the game, many important parameters for booting up are here, like screen size, the splash screen and the location of your story files.
* RenJSBootstrap: The bootstrap for RenJS, it sets up the splash screen and loading bar to let the player know resources are being loaded, and starts loading them.

```html
    <!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8" />
			<title> RenJS </title>
			<script type="text/javascript" src="libs/phaser.min.js"></script>
			<script type="text/javascript" src="config.js"></script>     
			<script type="text/javascript" src="RenJS/RenJSBootstrap.js"></script>
		</head>
		<body></body>
	</html>
```

## Config

The config file contains very important configuration parameters for starting the game. These are the minimal requirements to create the frame in the web page and start loading its contents.

```js
	var globalConfig = {
	  w:800,
	  h:600,
	  mode: "AUTO",
	  scaleMode: "SHOW_ALL", //SHOW_ALL, EXACT_FIT
	  splash: { //The "Loading" page for your game
	    loadingScreen: "assets/gui/splash.png", //splash background
	    loadingBar: {
	      fullBar: "assets/gui/loadingbar.png",
	      position: {x:111,y:462}
	    }
	  },
	  fonts: "assets/gui/fonts.css",
	  guiConfig: "story/GUI.yaml",
	  storySetup: "story/Setup.yaml",
	  //as many story text files as you want
	  storyText: [
	        "story/YourStory.yaml"
	    ],
	}
```
Let's check what each of these parameters mean:

* Screen size: w and h parameters are the resolution of the game, as width and height in pixels. You can use any resolution you want, but you'll have to make sure your GUI, backgrounds and other images matches with it.
* Mode: Phaser's rendering mode, unless you need to extend RenJS, you shouldn't touch this option.
* ScaleMode: It's related to the scaling of the game. The default option is "SHOW_ALL", that will scale the game to fit the whole screen (either in the computer or in a mobile device) but keeping the aspect ratio. Another interesting option could be "EXACT_FIT", that would strech the game to fit the screen, not keeping the aspect ratio.
* Splash: It's the image that will be shown while the game is loading. Depending on the size of the assets, it might take a while, so you can also add a loading bar, that will fill up from left to right to show the loading progress. If you show a bar, you will also need to specify where to show it, with the option "position".
* Fonts: This parameter specifies where to find the fonts.css file. This file is just to load your fonts onto the web page, and make it easier for Phaser to find it and use it to show all the texts in the game.
* Game scripts: guiConfig, storySetup and storyText are the files that make up your story, and usually, the files that will change the most (along with the assets) from story to story. You need to always have one guiConfig and storySetup, but you can have as many storyText files as you want. 

## RenJS

The files on the RenJS folder constitute the core of the game engine, the code that interprets your story and shows it to the players. The only one you need to take into account for now is RenJSBootstrap.js. This file is in charge of loading all the other .js files, and also every asset (images, music, etc) used by your game. If you know javascript programming and want to learn more about how it works, the [Engine](../engine) section has comprehensive documentation of the library.

## Other Libraries

The files on the libs folder are external libraries that RenJS needs to work properly, the most importan being PhaserJS, the "parent" engine, that provides the methods for showing images, playing music, etc. 

## The Story and its Assets

The assets folder contains all the resources used by your game. This includes the character images, backgrounds, music, etc, and also everything that makes up the GUI, like the menus backgrounds, buttons and everything else. This folder is not mandatory for every game, and neither is the structure followed by this quickstart. Your assets can be anywhere inside the root folder, and organized however you like.

Inside the story folder there are three .yaml files. As with the assets, you don't really need to have them inside this or any folder, but it's a good practice. These three files contain the story, its text and its configuration. You should have one GUI configuration file, one story setup file and as many story text files as you want. You can name these files whatever you like, and it'd be a good idea to have descriptive names for each one. The text of your story could be separated in many different files named after the sections of the game it contains, for example:

* intro.yaml
* path1.yaml
* path2.yaml
* endings.yaml

In the next chapter, we'll take a look at the contents of these three files.