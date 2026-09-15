# Yippy
macOS open source clipboard manager

![screenshot](images/screenshot.jpg)

Follow progress at <a href="https://yippy.mattdavo.com" target="_blank">yippy.mattdavo.com</a>

Read about the progress and learnings at <a href="https://yippy.mattdavo.com/blog" target="_blank">yippy.mattdavo.com/blog</a>

Find all releases at <a href="https://yippy.mattdavo.com/releases" target="_blank">yippy.mattdavo.com/releases</a>

## About this fork
This is a fork of [mattDavo/Yippy](https://github.com/mattDavo/Yippy), built from source to keep the app running after upgrading to **macOS 27 / Xcode 27**, where the upstream build (last released as an x86_64 dev build from 2021) no longer ran.

Changes made in this fork:
- Bumped `MACOSX_DEPLOYMENT_TARGET` to 12.0 — Xcode 27's SDK dropped support for the project's old 10.9–10.14 targets.
- Fixed a compile error in the `LoginServiceKit` pod caused by `LSSharedFileListCopySnapshot` now returning an optional in the macOS 27 SDK.
- Added explicit `import CoreGraphics` / `import ApplicationServices` where symbols (`CGKeyCode`, `AXIsProcessTrusted`, etc.) used to be pulled in transitively and no longer are.
- **Dropped x86_64/Intel support — this fork builds Apple Silicon (arm64) only.** The `ARCHS`/`VALID_ARCHS`/`EXCLUDED_ARCHS` build settings (project-level and in the `Podfile` `post_install` hook) are pinned to `arm64`. If you need to run on an Intel Mac, use [upstream](https://github.com/mattDavo/Yippy) instead.

**This fork has no releases or Homebrew Cask of its own** — it isn't published anywhere. `brew install --cask yippy` and the links/downloads below all point to the **upstream** project's official (Intel) build, not this fork. To get this fork's arm64 build, clone this repo and build it yourself in Xcode (see "Developing Yippy" below).

Everything below is the original upstream documentation.

## Installation
Downloaded from <a href="https://yippy.mattdavo.com" target="_blank">yippy.mattdavo.com</a> or install with [Homebrew Cask](https://github.com/Homebrew/homebrew-cask):
```
brew install --cask yippy
```

For help with installation see: <a href="https://yippy.mattdavo.com/installation" target="_blank">yippy.mattdavo.com/installation</a>.

## Developing Yippy
### Contributions
All contributions are welcome, whether they are pull requests, bug reports, feature requests or general feedback.

### Project Structure
There are 3 different schemes:
- Yippy
- Yippy Beta
- Yippy XCTest

__Yippy__ is used for running and archiving a production build of Yippy. __Yippy Beta__ is used for development and archiving a beta release. __Yippy XCTest__ is used exclusively for running the unit and UI tests.

### Using `create-installer.sh`
First install <a href="https://github.com/andreyvit/create-dmg" target="_blank">create-dmg</a>. Then place `X.app` in the same folder as `create-installer.sh`. Execute script:
```
./create-installer.sh X
```

You will find the installer disk image `X.dmg` in the same folder.

### TODO
- [ ] Support more types of pasteboard items
- [ ] Allow setting preferences for keyboard shortcuts
    - [x] Customize toggle hotkey
- [ ] Automatic updates (maybe use Sparkle?)
- [ ] Create a bug reporter, if places in code are reached that should not be possible create a unique error and a prompt to report the bug.
- [ ] Don’t let any of the app be used until access is granted
- [x] Toggle for attributed text
- [x] Launch at login
- [x] Convert history storage to storing each piece of data into a file organised by directory of indexes
- [ ] Favourites
- [ ] Search (https://github.com/krisk/fuse-swift)
- [x] Max history length
- [ ] Cell height cache improvements. Will improve window size changes and launch time.
    - [ ] Find a cheap way to clear the cell height cache
    - [ ] Store cell heights on disk
