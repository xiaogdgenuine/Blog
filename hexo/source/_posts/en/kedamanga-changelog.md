---
title: "Kedamanga Changelog"
date: 2023-10-25 23:20:05
tags:
- Kedamanga
---

## Version 2.0.0:
Features
- Now you can sync comics between devices with "iCloud Drive"
- Now you can sync reading histories, settings, bookmarks between devices with "iCloud"
- Now you can customize cover for all comics
- New "Random mode" feature can help you decide what comic book to read today :P

Fixes
- Fix some gesture conflicts in the Reader

## Version 1.7.2:
Features
- You can now long press empty area in Bookshelf to import files quickly

Fixes
- Fix EPUB file infinite loop bug when nested inside another archive

## Version 1.7.1:
Features
- Now you can turn off the「Downloads」folder in app setting, everything will save directly to the 「Library」

Fixes
- Fix private mode function crash on iOS 16 bug
- Fix clear reading history crash the app bug
- Fix a crash bug when sharing files on iPad
- Better support for EPUB files

## Version 1.7.0:
Features
- Redesigned control panel for reader
- You can now open PDF files with password protected
- Now the app support flip pages automatically

Fixes
- Fix a blurry bug when zoom in a large image
- Fix a bug that cause the private mode not working when device is locked

## Version 1.6.9:
Fixes
- Fix a bug that cause cover display delayed few seconds.

## Version 1.6.8:
Features
- Now you can double tap "Tab bar icon" and quickly go back to root view.
- You can now select and delete multiple reading records at once.
- Reading histories of「Download」folder will be showing Reading tab as well.

Fixes
- Fix a bug that cause reading progress lost during screen rotation.
- Fix a bug that cause reading history can't be delete.

## Version 1.6.7:
Features
- New layout option for Bookshelf - Card mode.

Fixes
- Fix scroll glitching in Bookshelf view
- Improve scroll performance for Bookshelf view

## Version 1.6.6:
Features
- Clear reading progress of a folder will clear all the reading history of it's nested items as well

Fixes
- Fix a bug that cause status bar never hide after switch to next comic book

## Version 1.6.5:
Features
- Add new "Default view when open app" option, you can now pick which view you want to see first after launch the app.
- You can now pinch to resize book size inside "Reading" tab, just like in Library.

Fixes
- Fix a bug that cause some reading progresses may not save properly.

## Version 1.6.3:
Features
- Support connect to Aliyundrive.
- Support RAR files with SFX module.
- A faster cache cleanup implementation.
- Support turning page by pageUp, pageDown key.

## Version 1.6.2:
Fixes
- Support solid rar files.
- Support filename encrypted rar files.

## Version 1.6.1:
Features
- You can now hide "Reading" tab, toggle it in setting.
- You can now disable "Double tap to zoom in" gesture in reader setting.
- Support reverse image order after split it.
- WiFi server now supports private mode.
- Support reading file in WebDAV server even if it doesn't support streaming reading.

Fixes
- Handle back slash properly in RAR files.
- Fix PDF file can't be open in WebDAV server issue.

## Version 1.6.0:
This time I bring you a fresh bookshelf, fix tons of crashes, as well as adding lots of enhancements.

Features
- Fresh new bookshelf.
- [Texture background] - makes you feel holding an real book.
- You can now pull to close the reader.
- New「Presets」setting to help you manage settings for multiple type of comics.

Fixes
- New PDF rendering engine, no content loss anymore!
- Improve memory usage, less crashing when openning big files.

## Version 1.5.2:
Features
- Image that can't fit into the page will now be put inside a scroll view.

Fixes
- Fix folder browser's back button missing issue in iOS 16.
- Fix an issue that cause some azw3 files to render duplicated.
- Fix an issue that cause pinch gesture freeze the app.

## Version 1.5.1:
Fixes
- Fix a bug that cause long comic image display in-position.

## Version 1.5.0：

I'm very sorry about taking so long yet just release a bug fix version, I'm still working on premier version.

For many reasons, I just can't done anything in the right time frame, always keep postpone schedules.

This year is definitely my toughest year so far, my dear father left me at a young age, 56. I still can't believe this just happened.

Anyway, life can be so suck, but one must fight back.

I will try to release regular bugfix versions before premier version is ready (let's try every 3 weeks first :)).

If you sent any feedback email and didn't get response from me, I owe you a sorry, I will start to respond some of feedback emails in next couple months.

Fixes
- Fix a crash issue when you enable 'image enhancement' at iOS 16.
- Fix a crash & white screen issue when open high resolution pictures, also improve the respond time when deal with high resolution pictures.
- Fix an issue that cause Mobi file to render duplicated page after reading about 1000 pages.


## Version 1.4.2
Features
- A fresh new 「Open last/next」 manga modal.
- Now you can open last/next manga directly in progress slider.

Fixes
- Fix a issue that cause the background music stopped when opening Kedamanga

## Version 1.4.1
Fixes
- Fix 301 error when connect to some WebDAV servers.
- Fix keyboard shortcut not working in iOS 15 issue.

## Version 1.4.0
Features
- Compatible with iPad mini6.
- Now you can browse directory content directly.
- Use same UI design for local Library and NAS server.
- RAR file now supports streaming reading too!
- You can now open a folder as a mangabook on NAS server.
- Press volume +, then volume - to open/hide private library.

Fixes
- Improve book thumbnail loading speed.
- Fix 401 error when connect to some WebDAV servers.
- Fix keyboard shortcut not working in iOS 15 issue.

Break Change
- Kedamanga now support iPad multitasking feature, you can use Kedamanga with other apps at the same time. But the cost is that you can't lock the screen orientation directly inside Kedamanga, you have to lock the device orientation by system menu.
