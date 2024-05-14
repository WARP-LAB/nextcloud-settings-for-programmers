# Nextcloud files sync configuration for programmers

## About

By default Nextcloud

* Does not sync hidden files (files having `.*` naming pattern) which are critical for coding projects.
* Synchronises unneeded large files that should be left out as they can be recreated on each machine instantly (`node_modules`, C/C++ compilation intermediate products, a.o.)
* Synchronises unneeded IDE caching, layout, logging etc. files.

This list tries to list all files that could/should be excluded when `Synch hidden files` option is turned on and offers a settings file that can be supplied to Nextcloud.

## Install custom patterns

See `sync-exclude.lst` contained in repo.

It includes all patterns discussed below.

To install:

* Quit *Nextcloud*
* Place `sync-exclude.lst` in correct location
  * macOS `~/Library/Preferences/Nextcloud/sync-exclude.lst` or (for older versions) `~/Library/Application\ Support/Nextcloud/sync-exclude.lst`
  * MSW10 `%AppData%\Nextcloud\sync-exclude.lst` or `%LocalAppData%\Nextcloud\sync-exclude.lst`
  * File may not exist in path after fresh install. Within Nextcloud *Settings* under *General* tab click *Edit Ignored files* to bring up modal - click *Restore Defaults*, it should create file and fill it with *Built in patterns* discussed below.
* Run *Nextcloud* client
* Pause synchronisation
* Within *Settings* under *General* tab click *Edit Ignored files* to bring up modal
* Enable *Sync hidden files*
* Check *Files ignored by patterns* list, it should include those specified in `sync-exclude.lst`
* Press OK
* Unpause synchronisation (or yet better, restart *Nextcloud* client once more)

## What to include

By allowing syncing of hidden files, we will sync

* Git - `.git` directories and all `.git*` conf files
* Web development stuff such as `.atomignore`, `.babelrc`, `.env`, `.eslintignore*`, `.eslintrc*`, `.rsyncexclude`, `.stylelintrc*` a.o.

## What to leave out

By allowing syncing of hidden files there are lots of hidden files that should be excluded anyways.
Apart from those we should make patterns to leave out also non-hidden files such as

* IDEs caches: Development on *Visual Code*, *Atom*, *Sublime*
* IDEs caches: C/C++/ObjC++ desktop and handheld development on *Xcode*, *Code::Blocks*, *Visual Studio*
* IDEs caches: C embedded development on *Eclipse*, *Visual Studio*
* IDEs caches: Old projects that used *NetBeans*
* Package manager directories, that are large, but can be easily recreated (i.e. `node_modules/`)
* Build side products
* OS cache, hidden files

## What should be left, but is not

A good example in case of programming is leaving out `*.obj` file sync. But we cannot, as extension is same as *Wavefront OBJ File* that we want to sync.

## Exclude - Built in patterns (static hardcoded)

These patterns are *Nextcloud* specific, they are static hardcoded, defined outside `sync-exclude.lst`.

| Pattern | Allow deletion | Description | Notes |
| ------- |:--------------:|:----------- |:----- |
| `.csync_journal.db*`      | | | |
| `._sync_*.db*`      | | | |
| `.sync_*.db*`      | | | |

## Exclude - Built in patterns

These patterns are set *out of box*. Meaning that a clean install of Nextcloud would put `sync-exclude.lst` in locations mentioned above and the file would have these patterns specified in it.

| Pattern | Allow deletion | Description | Notes |
| ------- |:--------------:|:----------- |:----- |
| **Current version** | | | |
| `*~`      | | BSD/nix | |
| `~$*`      | | | |
| `.~lock.*` | | file locking | |
| `~*.tmp` | | temporary files | |
| `*.~*` | Y | temporary files | |
| `Icon\r*` | Y | [icon folder, macOS](http://apple.stackexchange.com/a/31877) | |
| `.DS_Store` | Y | [dir attributes, macOS](https://en.wikipedia.org/wiki/.DS_Store) | |
| `.ds_store` | Y | [dir attributes, macOS](https://en.wikipedia.org/wiki/.DS_Store) | |
| `*.textClipping` | | text clipping, macOS | |
| `._*` | | file information, thumbnails for HFS+/Unix/UFS | |
| `Thumbs.db` | Y | image file caches, MSW | |
| `photothumb.db` | Y | thumbnails by PhotoScape | |
| `System Volume Information` | | NTFS related, MSW | |
| `.*.sw?` | | | |
| `.*.*sw?` | | | |
| `.TemporaryItems` | Y | temporary storage, macOS | |
| `.Trashes` | Y | trash temporary, macOS| |
| `.DocumentRevisions-V100` | Y | internal version control, macOS | |
| `.Trash-*` | Y | Linux trash folder, nix | |
| `.fseventd` | | filesystem events log, macOS | |
| `.apdisk` | | directories on remote AFP shares, created by macOS | |
| `.Spotlight-V100` | | macOS Spotlight index data | |
| `.directory` | | KDE directory preferences, nix | |
| `*.part` | | partial downloads | |
| `*.filepart` | | partial downloads | |
| `*.crdownload` | | partial downloads, Chrome | |
| `*.kate-swp` | | [Kate swap files](https://kate-editor.org) | |
| `*.gnucach.tmp-*` | | | |
| `*.synkron.*` | | [Synkron cache](http://synkron.sourceforge.net) | |
| `*.sync.ffs_db` | | [FreeFileSync db](http://www.freefilesync.org) | |
| `*.symform` | | [Symform files](http://symform.com) | |
| `*.symform-store` | | [Symform files](http://symform.com) | |
| `*.fuse-hidden*` | | FUSE mount leftovers | |
| `*.unison` | | [Unison locks](https://www.cis.upenn.edu/~bcpierce/unison/) | |
| `*.nfs` | | NFS mounting leftovers | |
| `.stfolder` | | [Syncthing marking](https://docs.syncthing.net/users/faq.html#how-do-i-serve-a-folder-from-a-read-only-filesystem) | |
| `.stignore` | | Syncthing ignores | |
| `.stversions` | | Syncthing versioning | |
| `My Saved Places.` | | Your Saved Places. | |
| `\#*#` | | emacs recovery files | |
| `*.sb-*` | | | |

## Exclude - Built in patterns (historic)

These patterns at some point were set *out of box*. They are reasonable and should be kept.

| Pattern | Allow deletion | Description | Notes |
| ------- |:--------------:|:----------- |:----- |
| **In previous versions (that should be excluded)** | | | |
| `desktop.ini` | | folder config file, MSW | |
| `.*.*.sw?` | | | |
| `*.nfs` | | NFS mounting leftovers | |

## Exclude - Custom patterns

| Pattern | Allow deletion | Description | Notes |
| ------- |:--------------:|:----------- |:----- |
| | | | |
| **macOS** | | | |
| `.fseventsd` | Y | macOS File System Events notification mechanism | |
| `.com.apple.timemachine.donotpresent` | Y | macOS | |
| `.AppleDouble` | Y | macOS | |
| `.LSOverride` | Y | macOS | |
| `.VolumeIcon.icns` | Y | icons, macOS | |
| `.AppleDB` | Y | directories on remote AFP shares, created by macOS | |
| `.AppleDesktop` | Y | directories on remote AFP shares, created by macOS | |
| `._.TemporaryItems` | Y | temporary storage, macOS | |
| `Network Trash Folder/` | | directories on remote AFP shares, created by macOS | |
| `Temporary Items/` | | directories on remote AFP shares, created by macOS | |
| | | | |
| **MSW** | | | |
| `ehthumbs.db` | Y | image file caches, MSW | |
| `ehthumbs_vista.db` | Y | image file caches, MSW | |
| `*.stackdump` | Y | image file caches, MSW | |
| `Desktop.ini` | Y | folder config file, MSW | Capitalised duplicate for built in pattern |
| `$RECYCLE.BIN/` | Y | Recycle Bin used on file shares, MSW | |
| `*.lnk` | Y | alias, MSW | |
| | | | |
| **BSD/nix** | | | |
| `.fuse_hidden*` | Y | alias, MSW | |
| | | | |
| **ANDROID** | | | |
| `.csettings` | Y | Android | |
| | | | |
| **Browser download partials** | | | |
| `.crdownload` | | Chrome and Edge | included in OOB patterns |
| `.part` | | Firefox | included in OOB patterns |
| `.opdownload` | | Opera | |
| `.partial` | | Internet Explorer 11 | |
| `.download` | | Safari | |
| | | | |
| **Node.js/NPM** | | | |
| `node_modules/`| Y | [dir for NPM](https://www.npmjs.com) | huge stuff, `package.josn` is synced, just do `npm i` |
| `.npm`| Y | NPM cache directory ||
| `.node_repl_history` | Y |  node.js REPL commands history | |
| `npm-debug.log*` | Y |  node.js logs | |
| `.lock-wscript` | Y | node-waf configuration | |
| | | | |
| **Bower** | | | |
| `bower_components/` | Y | [Bower components dir](https://bower.io) | `bower.json` is synced, just do `bower install` |
| `.bower-cache` | Y | [Bower junk](https://bower.io) | |
| `.bower-registry` | Y | [Bower junk](https://bower.io) | |
| `.bower-tmp` | Y | [Bower junk](https://bower.io) | |
| | | | |
| **Grunt** | | | |
| `.grunt` | Y | [Grunt cache](https://gruntjs.com) | |
| `.tmp/` | Y | [Grunt preprocess tmp dir](https://gruntjs.com) | |
| | | | |
| **Composer** | | | |
| `vendor/` | | [Composer](https://getcomposer.org) | `composer.json` is synced, so just do `composer install`. ***Beware, this is aggressive exclude - generic dir name, so some stuff that is not *Composerish* might not be synced!** |
| | | | |
| **Sass** | | | |
| `.sass-cache/` | Y | [Sass](https://sass-lang.com) cache |  |
| | | | |
| **Sublime Text** | | | |
| `*.tmlanguage.cache` | Y | [Sublime Text cache](https://www.sublimetext.com) | |
| `*.tmPreferences.cache` | Y | [Sublime Text cache](https://www.sublimetext.com) | |
| `*.stTheme.cache` | Y | [Sublime Text cache](https://www.sublimetext.com) | |
| `*.sublime-workspace` | Y | [Sublime Text cache](https://www.sublimetext.com) | workspace files are user-specific |
| | | | |
| **Xcode, Clang** | | | |
| `*~.nib` | Y | Xcode | |
| `*.swp` | Y | Xcode | |
| `*.out` | Y | Xcode | **Beware, this is aggressive exclude** |
| `*.pbxuser` | Y | Xcode | workspace files are user-specific |
| `*.perspective` | Y | Xcode | workspace files are user-specific |
| `*.perspectivev3` | Y | Xcode | workspace files are user-specific |
| `*.mode1v3` | Y | Xcode | workspace files are user-specific |
| `*.mode2v3` | Y | Xcode | workspace files are user-specific |
| `*.user` | Y | Xcode | workspace files are user-specific |
| `xcuserdata/` | Y | Xcode | exclude `xcuserdata` |
| `*.xcworkspace` | Y | Xcode | keep out for now |
| `*.xccheckout` | Y | Xcode | workspace files are user-specific |
| `*.buld/` | Y | Xcode | |
| `*.hmap` | Y | Clang header map | |
| `dgph` | Y | dependency graph information | |
| `*.d` | Y | header dependencies | |
| `*.dia` | Y | serialised diagnostics blob | |
| `*.LinkFileList` | Y | what it says | |
| `*_dependency_info.dat` | Y | contains all libs, frameworks that are linked | |
| | | | |
| **Visual Studio, MSVC** | | | |
| `*.sdf` | Y | Visual Studio | |
| `*.opensdf` | Y | Visual Studio | |
| `*.suo` | Y | Visual Studio | |
| `*.pdb` | Y | Visual Studio | **Beware, same as Protein Data Bank file** |
| `*.ilk` | Y | Visual Studio | |
| `*.aps` | Y | Visual Studio | |
| `*.ncb` | Y | Visual Studio | |
| `ipch/` | Y | Visual Studio | |
| `*.tlog/` | Y | Visual Studio | |
| `*.tlog` | Y | Visual Studio | |
| `*.lastbuildstate` | Y | Visual Studio | |
| `*.idb` | Y | MSVC++ | |
| | | | |
| **Visual Code** | | | |
| `.history` | Y | Visual Code local history of files | |
| **Platform.io** | | | |
| `.pio/` | Y | | |
| `.pioenvs/` | Y | | |
| `.piolibdeps/` | Y | | |
| | | | |
| **Code::Blocks** | | | |
| `*.depend` | Y | Code::Blocks | |
| `*.layout` | Y | Code::Blocks | workspace files are user-specific |
| | | | |
| **Eclipse** | | | |
| `.metadata` | Y | Eclipse | |
| `local.properties` | Y | Eclipse | |
| `.externalToolBuilders` | Y | Eclipse | |
| | | | |
| **Others** | | | |
| `pids/` | | runtime data | |
| `*.pid` | Y | runtime data | |
| `*.seed` | Y | runtime data | |
| | | | |
| `*.o` | | build products | **Beware, this is aggressive exclude** |
| `*.idb` | | build products | **Beware, this is aggressive exclude** |
| `*.mode*` | | build products | **Beware, this is aggressive exclude** |
| `*.dSYM` | | build products | **Beware, this is aggressive exclude** |
| `*.pyc` | | build products | **Beware, this is aggressive exclude** |
| | | | |
| `*.cpp.eep` | | | **Beware, this is aggressive exclude** |
| `*.cpp.elf` | | | **Beware, this is aggressive exclude** |
| `*.cpp.hex` | | | **Beware, this is aggressive exclude** |

## Do not exclude

| Pattern | Allow deletion | Description | Notes |
| ------- |:--------------:|:----------- |:----- |
| `.htaccess` | | [Apache configuration files](https://httpd.apache.org/docs/current/howto/htaccess.html) | When Nextcloud is run by Nginx (or even in the case of Apache if `datadirectory` is outside webroot) it is safe to allow syncing `.htaccess`. [*1] |

[*1]
Remeber to remove `'.htaccess'` in Nextcloud's `config.php` from blacklist

```php
  // default implicit
  // 'blacklisted_files' => ['.htaccess'],
  // by setting empty array .htaccess is allowed
  'blacklisted_files' => [],
```

## Todo

* Redo all Visual Studio / MSVC stuff
* Check file patterns for VisualGDB junk files.
* Suggest rule importing menu in *Nextcloud* client app Settings that can take lists in `LST` (`CSV`/`XML`) format and replace and/or merge it with existing whatever settings. It is not so much about user friendly way to add patterns, it is more about merging patterns. Say your team start using new app/tech that generates files you want to exclude - just generate patterns ignore list and send out to everybody in the workgroup.
