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
  wine-base-stable:
    interface: content
    target: $SNAP/wine-platform
    default-provider: wine-platform
```
Here's an example that shows how to use some of the capabilities outlined above:

* Here `wine-base-stable` plug is used by user snap to connect it's plug to `wine-platform` snap
* `wine-platform` snap each plug have different WINE versions
* `wine-base-stable` uses `wine-stable`
* `wine-base-devel` uses `wine-devel`
* `wine-base-staging` uses `wine-staging`
*  only one `WINE` base per snap is used
* In target `$SNAP/wine-platform` where `wine-base` data will be mounted though Developers have to ship that empty DIR in `root` `PATH` of their snaps

## Connecting the plugs
* Well plug connection should be automate with the base snap when installing the user snap that has plugs properly defined if not then use below command to connect `foo` snap to wine platform snap manually with `wine-base-stable` slot of `wine-platform` to use `wine-stable`


```
snap connect foo:wine-base-stable wine-platform:wine-base-stable
```

_________________________________________________________________

**Check `snapcraft.yamls` for further refrences**

[notepad-plus-plus](https://raw.githubusercontent.com/mmtrt/notepad-plus-plus-snap/refs/heads/master/snap/snapcraft.yaml) - [notepad3](https://raw.githubusercontent.com/mmtrt/notepad3/refs/heads/master/snap/snapcraft.yaml)

If you have any questions about creating snaps of WINE compatible
Windows applications then [post in the Snapcraft forum](https://forum.snapcraft.io).
