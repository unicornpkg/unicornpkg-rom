## Server resource pack for computercraft

### Description
This is an example of a server resource pack made to modify the `rom` folder on a Minecraft modded server with computercraft.
It is an easy way to modify the mod computercraft in an non-invasive way, since modifying the pack itself on server side may corrupt the modpack.

### Pack hierarchy
If no precision is given, the naming of the folders **must** be kept.

cc-pack/ : the name of the pack, can be changed to anything you want

cc-pack/assets/ : root of the pack, can contain other mods folders
cc-pack/cc-pack.zip : the pack itself when compressed in .zip format, this is the pack that will be on server and client side
cc-pack/pack.mcmeta : description of the pack, content can be modified (see minecraft doc for more information)
cc-pack/pack.png : image of the pack

cc-pack/assets/computercragt/lua/rom/ : anything that is put there will override (if the file already exist in the rom) or will be added to the rom when the pack is on the server

Warning :
cc-pack/assets/computercragt/lua/rom/startup : be really cautious when modifying this file, it is the native startup of all computers, if it is corrupted then it will break all new computers put in the world, I recommend deleting it except if you really know what you are doing

### How to create and deploy the pack ?
You can test your pack with a computercraft emulator such as cc-emux before testing it on the server, that will save you a lot of time if you develop the pack.

When you think your pack is ready to be tested on your server you have to :
[FOR THE SERVER]
- put the folder of the pack (`cc-pack` in this case) + the files `pack.mcmeta` and the icone of the pack (`pack.png` in this case) in a .zip archive
- copy the pack (in .zip format) in the `resourcepacks/` folder on your server (if it doesn't exist then create it at the root of the server) 

[FOR THE CLIENT]
- upload the file on the cloud, I recommend using dropbox which creates a permanent link to the file while you don't change it's name and you just need to put the file in a folder that is sync with dropbox (compression and upload can then be automated with a script)
- [only once] copy the http link to the uploaded file, make sure it's a link that **download the file immediately when clicking on it** (so for dropbox make sure it ends with "1") and put this link in the `server.properties` at the line `resource-pack=`, example : `resource-pack=https://www.dropbox.com/s/jhqaufjr94hw0y3/cc-pack-live.zip?dl=1`

You probably noticed but even for the client side the players don't have to do any specific stuff, when they connect to the server they will be prompted to accept to download the resource pack, if they don't it will not prevent them from playing and even using computercraft.

### Example of script to compress the file (for automation purpose)
You can adapt this script to automate the .zipping of the pack, make sure to use different names of files for "in development" and "in production" packs.
```bat
rem prod
rem tar.exe -acf "<path to dropbox folder>\cc-pack.zip" cc-pack/*

rem dev
tar.exe -acf "<path to dropbox folder>\cc-pack-dev.zip" cc-pack/*

rem 
tar.exe -acf "<path to your client resource packs>\cc-pack.zip" cc-pack/*
```

## Warnings
Modifying a mod this way can break the new computers put in the world after adding the resource pack (server side), if so you can simply remove the pack from the server folder.