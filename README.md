<h1 align="center">
  <br />
  Wine Platform
</h1>

<p align="center"><b>wine platform snap that provides WINE base for win application snaps</b>. Snap developers that create WINE snaps can leverage this base snap to connect it to their WINE snaps.</p>

## Using this snap base

You can use this snap as a reference for creating snaps of other WINE
compatible 32-bit Windows applications or games. Here are the main
things you'll need to use in your snaps:


## Getting plugs to user snap

* Adding content interface plug in snapcraft.yaml

```
plugs:
  wine-platform-plug:
    content: wine-base-stable
    interface: content
    target: $SNAP/wine-platform
    default-provider: wine-platform

apps:
  foo:
   command: bar
   plugs:
    - wine-platform-plug
```
Here's an example that shows how to use some of the capabilities outlined above:

* Here `wine-platform-plug` is used by user snap to connect it's plug to `wine-platform` snap
* In content `wine-base-stable` uses the slots of ``wine-platform` each slot has different WINE versions
* `wine-base-stable` uses `wine-stable`
* `wine-base-devel` uses `wine-devel`
* `wine-base-staging` uses `wine-staging`
*  only one `WINE` base per snap is used
* In target `$SNAP/wine-platform` where `wine-base` data will be mounted though Developers have to ship that empty DIR in `root` `PATH` of their snaps

## Getting wine-base env PATHs to user snap
* defining wine base paths in WINE env on snap wrapper script

```
export WINEVERPATH=$SNAP/wine-platform/wine-stable
export WINESERVER=$SNAP/wine-platform/wine-stable/bin/wineserver
export WINELOADER=$SNAP/wine-platform/wine-stable/bin/wine
export WINEDLLPATH=$SNAP/wine-platform/wine-stable/lib/wine/fakedlls
export WINETRICKS=$SNAP/wine-platform/bin/winetricks

export LD_LIBRARY_PATH="$SNAP/wine-platform/lib:$SNAP/wine-platform/lib/$ARCH:$SNAP/wine-platform/usr/lib:$SNAP/wine-platform/usr/lib/$ARCH:$LD_LIBRARY_PATH"

export PATH=$PATH:$SNAP/wine-platform/bin:$SNAP/wine-platform/usr/bin:$SNAP/wine-platform/wine-stable/bin
```
* Here target`PATH``$SNAP/wine-platform` earlier defined in plugs is used as well as the `wine-base` which has full `PATH` `$SNAP/wine-platform/wine-stable` which can be different depending on `wine-base-xxxxx` used by the snaps so in this exp we are using `wine-base-stable`
* Developers should use the target `PATH` in other libraries `CONFIG` env

## Connecting the plugs
* Well plug connection should be automate with the base snap when installing the user snap that has plugs properly defined if not then use below command to connect `foo` snap to wine platform snap manually with `wine-base-stable` slot of `wine-platform` to use `wine-stable`


```
snap connect foo:wine-platform-plug wine-platform:wine-base-stable
```

_________________________________________________________________

**Check out wrapper scripts that are using this snap env**

[notepad-plus-plus](https://raw.githubusercontent.com/mmtrt/notepad-plus-plus/master/scripts/notepad-plus-plus) - [cncra](https://raw.githubusercontent.com/mmtrt/cncra/master/snap/scripts/sommelier)

**Also check `snapcraft.yamls` for further refrences**

[notepad-plus-plus](https://raw.githubusercontent.com/mmtrt/notepad-plus-plus/master/snap/snapcraft.yaml) - [cncra](https://raw.githubusercontent.com/mmtrt/cncra/master/snap/snapcraft.yaml)

If you have any questions about creating snaps of WINE compatible
Windows applications then [post in the Snapcraft forum](https://forum.snapcraft.io).
