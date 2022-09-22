**This project is an informal one, produced by an individual.**

[Github](https://github.com/warai-bukuro/steamcmd-arm64/blob/master/README.md)

# Supported tags and respective `Dockerfile` links
  -	[`root` (*bullseye-root/Dockerfile*)](https://github.com/CM2Walki/steamcmd/blob/master/bullseye-root/Dockerfile)

# What is SteamCMD?
The Steam Console Client or SteamCMD is a command-line version of the Steam client. Its primary use is to install and update various dedicated servers available on Steam using a command-line interface. It works with games that use the SteamPipe content system. All games have been migrated from the deprecated HLDSUpdateTool to SteamCMD. This image can be used as a base image for Steam-based dedicated servers (Source: [developer.valvesoftware.com](https://developer.valvesoftware.com/wiki/SteamCMD)).

# How to use this image
Whilst it's recommended to use this image as a base image of other game servers, you can also run it in an interactive shell using the following command:
```console
$ docker run -it --name=steamcmd cm2network/steamcmd bash
$ ./steamcmd.sh +force_install_dir /home/steam/squad-dedicated +login anonymous +app_update 403240 +quit
```
This can prove useful if you are just looking to test a certain game server installation.

Running with named volumes:
```console
$ docker volume create steamcmd_login_volume # Optional: Location of login session
$ docker volume create steamcmd_volume # Optional: Location of SteamCMD installation

$ docker run -it \
    -v "steamcmd_login_volume:/home/steam/Steam" \
    -v "steamcmd_volume:/home/steam/steamcmd" \
    cm2network/steamcmd bash
```
This setup is necessary if you have to download a non-anonymous appID or upload a steampipe build. For an example check out:
https://hub.docker.com/r/cm2network/steampipe/

## Configuration:
This image includes the `nano` text editor for convenience. 

The `steamcmd.sh` can be found in the following directory: `/home/steam/steamcmd`

## Examples:
Consult the following repositories for examples on how to base an image off of this one:<br/>
https://hub.docker.com/r/cm2network/squad/<br/>
https://hub.docker.com/r/cm2network/csgo/<br>
https://hub.docker.com/r/cm2network/mordhau/

# Image Variants:
The `steamcmd` images come in two flavors, each designed for a specific use case.

## `steamcmd:root`
This is a specialized image. This image's default user is `root`. If you need to install additional packages for you game server and do not want to create excess layers, then this is the right choice.

_Note: Running the `steamcmd.sh` as `root` will fail because the owner is the user `steam`, either swap the active user using `su steam` or use chown to change the ownership of the directory._
