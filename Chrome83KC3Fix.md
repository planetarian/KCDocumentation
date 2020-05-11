# Chrome v83 KC3 Fix
There exists a bug(?) in Chrome version 83 which causes KC3's devtools panel to fail to load when you open the game.

It is easy to work around this by simply closing and reopening devtools, but you must remember to do this on every F5 as well, otherwise your KC3 will appear to be functional but will not update when you perform game actions.

This creates the potential for accidents, so more effective workarounds have been investigated.

## The issue

An issue with Chrome 83's Site Isolation feature (intended to protect against i.e. Spectre) causes the chrome devtools network API to stop firing events when content from a different origin is loaded in an iframe.

Since KanColle itself is loaded in an iframe on DMM.com, this triggers the bug.

(see bug report at https://bugs.chromium.org/p/chromium/issues/detail?id=1081270 )

## The fix

### Option A: Disable Site Isolation
The simplest fix is to disable Site Isolation. You can do this by navigating to `about:flags/#site-isolation-trial-opt-out` in your browser and setting the 'Disable site isolation' option to 'Disabled'.

Remember, Site Isolation is a security feature. Disabling it could leave you potentially vulnerable to certain types of attacks if you're not careful.

### Option B: Disable Updates
If you're already on a version earlier than 83, you can try disabling the auto-update mechanism. Unfortunately, Chrome doesn't make it easy to disable updates.

Of course, disabling updates comes with the caveat of not being able to receive new security features when they're published, so if you choose this route, you should only keep updates disabled until the bug has been reported as fixed.

#### Disabling GoogleUpdate.exe
No method is guaranteed, but the usual recommended method is to disable the `GoogleUpdate.exe` service. You can do this via `taskmgr`, `msconfig`, `services.msc`, or `regedit`, if you know what you're doing.

#### Using registry policies
You can also try using registry policies to disable updates, but this depends on Chrome actually listening to the policies in question.

A registry file to perform this step for you can be found here (right-click -> save link):
https://raw.githubusercontent.com/planetarian/KCDocumentation/master/Chrome83KC3Fix/DisableChromeUpdates.reg

### Option C: Install Chromium
Alternatively, you can use an alternative version of Chrome that doesn't update automatically, such as Chromium.

This may be the most ideal option, as you can use this alternative browser purely for KC while your everyday browsing remains secure.

You can find a stable build of Chromium v81 here: https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Win_x64%2F737173%2Fchrome-win.zip?generation=1580439619624464&alt=media
