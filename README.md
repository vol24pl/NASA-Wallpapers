# NASA Wallpapers
MacOS script to fetch NASA's [Astronomy Picture of the Day](https://apod.nasa.gov/apod/astropix.html) and set it as a wallpaper. It can be used to **automagically fetch a new wallpaper each day 🪄✨**

## Linux? Windows?
This script can be easly repurposed for other operating systems. For POSIX systems you just need to replace the AppleScript (`osascript`) part with the os specific equivalent. For Windows you can try with Windows Subsystem for Linux. If you actually make it, please fork this and post a pull request 🥺

## macOS Script

```zsh
sleep 10 && curl $(echo "https://apod.nasa.gov/apod/$(curl https://apod.nasa.gov/apod/astropix.html | grep -m 1 "png\|jpg\|jpeg" | awk -F '"' '{print $2}')") > /var/tmp/new-wallpaper && osascript -e 'tell application "Finder" to set desktop picture to POSIX file "/var/tmp/new-wallpaper"'
```
**This script:**

1. Waits 10 seconds. Important, if it's used at booting Mac. You don't want to do it instantly, before (more important) macOS services are fully working.
2. Goes into https://apod.nasa.gov/apod/astropix.html website and downloads the HTML code of the main site.
3. Scanns the code for the first accurance of the PNG/JPG/JPEG files and glues together URL for that image.
4. Downloads the image into `/var/tmp` folder (system's temporary folder).
5. Uses AppleScript to set up the background image. This step requires permissions to control computer. AppleScript is an Apple scripting language to control UI Applications by commands, and can be easily abused. Always verify AppleScript (`osascript`) you are executing. Fortunately this part of the script almost reads as English so you can verify it with little to no coding abilities 🤓

## How to make it run on each boot

### Just use the script
Just use it with crontab or launch deamon 😎

### DIY Automator App

1. Open Automator, create a new Application
2. Drag and drop "Run Shell Script"
3. Remove everything from textbox and paste the script
4. Save it as NASA-Wallpapers.app
5. (Optional) Copy NASA-Wallpapers.app to Applications folder
6. Go to System Settings -> General -> Login Items
7. Add NASA-Wallpapers.app as Login Item

### Prebuild Automator App

1. Download [pre-made App](https://github.com/vol24pl/NASA-Wallpaper/blob/main/NASA-wallpapers.zip) and unzip it
2. (Optional) Copy it to Applications folder
3. (Optional) Open it inside the Automator.app and make sure the script inside is correct!
4. Go to System Settings -> General -> Login Items
5. Add it as Login Item

## Warning ⚠️
Sometimes NASA uploads non-image media, such as youtube videos. In this cases the script obviously won't work properly. Just wait for another day 😆

|![Example of youtube video media](./video-example.png)|
|:--:|
|*Example of Youtube video media from May 31, 2023*|
