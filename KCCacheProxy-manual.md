To install the Electron version of KCCacheProxy without having to run the installation exe (allowing you to place the application files wherever you like):

1) Install 7-zip:

32-bit: https://www.7-zip.org/a/7z1900.exe

64-bit: https://www.7-zip.org/a/7z1900-x64.exe


2) Download the KCCacheProxy installer:

https://github.com/Tibowl/KCCacheProxy/releases/download/v2.3.1/KCCacheProxy-2.3.1.Setup.exe

3) Find the KCCacheProxy installer you downloaded, right-click it, find `7-zip->Open archive` in the menu:

![Open the installer as an archive](/KCCacheProxy-manual/01.png)
  
4) 7-zip will open, showing the installer's contents. Find `KCCacheProxy-2.3.1-full.nupkg`, right-click it, click `Open Inside`:

![Open the KCCacheProxy nupkg file](/KCCacheProxy-manual/02.png)

5) Open the `lib` folder in the list that appears.

![Open the lib folder](/KCCacheProxy-manual/03.png)

6) Click the `net45` folder, and click `Extract` in the main toolbar.

![Extract the net45 folder](/KCCacheProxy-manual/04.png)

7) Provide a location to extract the files to.

8) Open the extracted `net45` folder in Windows Explorer, and click `KCCacheProxy.exe` to launch.

![Open KCCacheProxy](/KCCacheProxy-manual/05.png)
