---
layout: post
date:   2021-04-01 14:21:00 +0100
categories: jekyll
---

# How to get install Jekyll on Windows 10 with Ruby DevKit 3.0
1. Go to [the Ruby installation page](https://rubyinstaller.org/downloads/)
2. Download the latest version of Ruby (At this point version 3.0.0-1 (x64)
3. Run the installer.
	1. At the end you'll get the option to run ridk (Do it)

```powershell
ridk install
```
 4. Close the console completely once you've installed it, reopen it then run the following command to make sure Jekyll is installed

```powershell
jekyll -v
```

5. Once you've done this, run the following command - If you don't iinstall Webrick you won't be able to run 'jekyll serve --watch'

``` powershell
bundle add webrick
```

This will probably be fixed in a later version.