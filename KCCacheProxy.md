# KCCacheProxy
   ![KCCacheProxy icon](/KCCacheProxy/200403_asashiofairy_sm.png)
   
This is an app by Tibo which sits between you and the game servers, and acts as a
second cache. It greatly reduces the amount of time spent downloading game assets
from the KanColle servers, and generally improves the responsiveness of the game.

The proxy also allows players outside Japan to bypass the current foreign IP block.

No game files are modified in the process.


## Installing/starting the proxy (Windows):

Download and install `KCCacheProxy-<version>.Setup.exe` from https://github.com/Tibowl/KCCacheProxy/releases

## Setting up the cache

You have the option of either starting from a minimal cache, containing only the most crucial set of starting files, OR you can start from a full cache dump, which is 4+ GB and may take some time to download.

If you start from the full cache dump, the proxy will have almost all game files already cached when you play. If you start from the minimal cache, the cache will initially be empty, and will be built up as you play.

### Option A: Minimal cache:

Open KCCacheProxy from your start menu, configure the options as desired.

(Recommended: check `Start in system tray` and `Bypass checking for gadget updates`.)

Click `Import built-in basic cache dump`, and click `Save`.

   ![Importing basic cache dump](/KCCacheProxy/A10.png)
   
### Option B: Full cache dump:

1) Download the latest full cache dump `cache-YYYY-MM-DD.zip` (verify the date), and optionally, all of the the `cache-diff-YYYY-MM-DD-to-YYYY-MM-DD.zip` files with dates *after* that, from one of these sources:

   MEGA: https://mega.nz/#F!sOwClABa!yHldyYZr2MBqhTNYEupztg
   
   Mirror: http://shizuru.piro.moe/kccp/
   
2) Open KCCacheProxy from your start menu, and click the `Import cache dump` button (*not* `Import built-in basic cache dump`!).

3) Select the `cache-YYYY-MM-DD.zip` file you downloaded in step #1, and click Open.

4) The import process may take some time, and the window may appear to freeze in the meantime. This is normal. Wait for the message in the proxy log confirming success of the cache dump import.

5) Repeat steps 2 through 4 for each of the `cache-diff-...` files downloaded in step #1, *in order from oldest to newest*.

6) Configure the rest of the options as desired.

(Recommended: check `Start in system tray` and `Bypass checking for gadget updates`.)

7) Click `Save`.

   ![Configuring full cache dump](/KCCacheProxy/A12.png)

### After cache has been configured

You may now close the window, and it will continue running in your system tray.
It should start automatically with Windows; if it does not appear in the system tray after you start Windows, you can launch it from the start menu.
 
## Enabling proxy for Chrome/KC3:

1) Install the browser extension ProxySwitch Omega:
   https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif

2) You should have a little circle icon for ProxySwitch Omega next to the browser's
   address bar. Click it, and click `Options`. It will try to guide you
   through stuff, feel free to click your way through or skip the tutorial messages.

   ![Accessing ProxySwitch Omega options](/KCCacheProxy/B2.png)

3) In the options screen, on the left menu, under `Settings`, select `Import/Export`. 
4) Enter the following address in the `Restore from online` field:
   https://raw.githubusercontent.com/Tibowl/KCCacheProxy/master/misc/OmegaOptions.bak
5) Click `Restore`.

   ![Configuring proxy server](/KCCacheProxy/A11.png)

6) Click ProxySwitch's circle icon next to the address bar again,
   and click `Auto Switch`.

   ![Activating the proxy connection](/KCCacheProxy/B8.png)

7) Restart your browser.


## Playing with proxy

If everything worked, after you restart your browser and attempt to access the game,
you will begin seeing `GET:` messages in the console (if you have it visible).
If you see `403` messages, this is normal.

   ![Normal proxy operation](/KCCacheProxy/C1.png)

### Notes
*You must leave the proxy running while you play.*
If you exit the proxy, your game will not work.
If you want to play without the proxy, click the ProxySwitch Omega icon in your browser,
and click `[System Proxy]`:

   ![Disabling proxy](/KCCacheProxy/C2.png)
