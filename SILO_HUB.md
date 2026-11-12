# Silo Hub

One app, one App ID, for every Silo app, that can still install any IPA that is not in the Silo list.

Silo Hub is a fork of [LiveContainer](https://github.com/LiveContainer/LiveContainer) (AGPL-3.0, so this
repo stays AGPL-3.0 and its source stays available). LiveContainer runs other apps inside itself, so the
free Apple ID limits (3 active apps, 10 App IDs per 7 days) apply to the hub alone, not to each app.

## What it is for

- **Silo apps** (Gallery, Drive, Lyrics, later Notes, AI and friends' apps) are listed in the Silo source
  feed and installed from inside the hub with one tap.
- **Anything else**: import an IPA from Files or a link, or add another AltStore source. Nothing in the hub
  depends on an app being listed.
- **Self-update** (standing rule): the hub shows its version, checks the Silo feed on open and in the
  background, and installs its own update with as little asking as iOS allows.
- **Refreshing** the hub and its apps is done by the built-in SideStore that ships in the
  LiveContainer+SideStore build.

## Plan

1. Prove CI: build the untouched upstream on a runner we can use.
2. Rebrand: name Silo Hub, bundle `com.bigbahar.silohub`, icon, Silo look (charcoal dark, cyan accent,
   Front page light, Rubik), no browser or OS default controls.
3. Source: preload `https://bigbahar.github.io/silo-store/source.json` as the Silo source.
4. Self-update from the Silo feed (version row, check on open, background check, install).
5. Port the tunnel work from Silo Store (LocalDevVPN switching, Tailscale relay mode) into the built-in
   SideStore.
6. Silo apps that need an extension (Lyrics Live Activity): the hub ships one shared Live Activity
   extension; guest apps cannot register their own.

## Known limits (from LiveContainer)

- Guest apps cannot have their own app extensions, widgets, Live Activities or remote push.
- Permissions are granted to the hub once and shared by all guest apps.
- Guest app containers are not sandboxed from each other.
- Not yet tested on iOS 27.0.1 with a free Apple ID. That is the first thing to verify on the phone.

## Upstream

`upstream` is LiveContainer/LiveContainer. Merge from it with `git fetch upstream && git merge upstream/main`.
