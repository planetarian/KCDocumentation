# KCCacheProxy
This is an app by Tibo which sits between you and the game servers, and acts as a
second cache. It greatly reduces the amount of time spent downloading game assets
from the KanColle servers, and generally improves the responsiveness of the game.

The proxy also allows players outside Japan to bypass the current foreign IP block.

No game files are modified in the process.


## Installing/starting the proxy (Windows):

1) Download and install the proxy:

   https://github.com/planetarian/KCCacheProxy/releases/download/v1.6/KCCacheProxy-win.zip

## Setting up the cache

You have the option of either starting from a minimal cache, containing only the most crucial set of starting files, OR you can start from a full cache dump, which is 4+ GB and may take some time to download.

If you start from the full cache dump, the proxy will have almost all game files already cached when you play. If you start from the minimal cache, the cache will initially be empty, and will be built up as you play.

### Option A: Minimal cache:

Open KCCacheProxy from your start menu, configure the options as desired (Recommended: check 'Start in system tray'), and click "Import built-in basic cache dump".

   ![Importing basic cache dump](/KCCacheProxy/A10.png)
   
### Option B: Full cache dump:

1) Download `cache-2020-03-07.zip`:

   https://mega.nz/#!MLRwEAQA!LRTokFd1enTCU35D6u1pS3k5eoutcX_H7WjNw521_VI
   
2) Open Windows Explorer and navigate to `%AppData%\KCCacheProxy\ProxyData` via your address bar.
   Extract the `cache-2020-03-07.zip` here. this should create a `cache` folder.

3) Back in the KCCacheProxy window, click 'Reload Cache'.

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

3) In the options screen, on the left menu, under Profiles, select `proxy`.
4) Under `Proxy Servers`, set the `Server` field to `127.0.0.1`,
   and the `Port` field to `8081`, then click `Apply Changes` on the left.

   ![Configuring proxy server](/KCCacheProxy/B4.png)

5) On the left menu, under `Profiles`, select `auto switch`.
6) You will see some default entries in the page that appears; delete these
   and use the `Add condition` button to add the following three entries,
   replacing `yourserverip` with your KC server's IP address:
```      | Condition Type | Condition Details          | Profile
      | URL wildcard   | http://yourserverip/kcs/*  | proxy
      | URL wildcard   | http://yourserverip/kcs2/* | proxy
      | URL wildcard   | http://203.104.209.7/*     | proxy
```
   You can find your server's IP address by looking up your server here:
   https://kancolle.fandom.com/wiki/Servers

   ![Configuring proxy traffic](/KCCacheProxy/B6.png)

7) Click `Apply changes` on the left.
8) Click ProxySwitch's circle icon next to the address bar again,
   and click `auto switch`.

   ![Activating the proxy connection](/KCCacheProxy/B8.png)

9) Restart your browser.


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
