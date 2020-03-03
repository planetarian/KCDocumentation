# KCCacheProxy
This is an app by Tibo which sits between you and the game servers, and acts as a
second cache. It greatly reduces the amount of time spent downloading game assets
from the KanColle servers, and generally improves the responsiveness of the game.

The proxy also allows players outside Japan to bypass the current foreign IP block.

No game files are modified in the process.


## Installing/starting the proxy (Windows):

1) Download `KCCacheProxy-win.zip`:

   https://github.com/planetarian/KCCacheProxy/releases/download/v1.1/KCCacheProxy-win.zip

2) Download `cache-2020-02-28.zip`:

   https://mega.nz/#!lPxTzLIC!-PsXIeVqVM1o9iZPCRp4ruQ--KlYWVKxSG7awF5qUbU

3) Extract `KCCacheProxy-win.zip` somewhere. Doesn't matter where;
   `Downloads` folder is fine. You should now have a `KCCacheProxy-win` folder.
   
   ![Right click the file and click 'extract'](/KCCacheProxy/A4.png)
   
   ![Then extract to your Downloads folder, or wherever](/KCCacheProxy/A4b.png)

4) Open the `KCCacheProxy-win` folder, you should see a number of files.
   Extract the `cache-2020-02-28.zip` here. this should create a `cache` folder.
   Your `KCCacheProxy-win` folder contents should now look like this:
   
   ![KCCacheProxy-win folder contents](/KCCacheProxy/A5.png)

5) Open `proxy-win.exe`. Accept the firewall request if prompted.

The proxy app will appear as an icon in your system tray.
If you don't see the icon, it may be hidden; click the arrow next to the system tray
to see hidden icons.

   ![System tray icon](/KCCacheProxy/A9.png)

You can use this icon (via right-click menu) to show the console, or close the proxy.
Note that the minimize/close buttons on the console window *will not* send it back to
the system tray; you must use the system tray menu for this.

 
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
you will begin seeing `GET:` messages in the console. If you see `403` messages, this is normal.

   ![Normal proxy operation](/KCCacheProxy/C1.png)

### Notes
*You must leave the proxy running while you play.*
If you exit the proxy, your game will not work.
If you want to play without the proxy, click the ProxySwitch Omega icon in your browser,
and click `[System Proxy]`:

   ![Disabling proxy](/KCCacheProxy/C2.png)
