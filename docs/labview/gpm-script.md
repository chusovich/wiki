# GPM
see packages and docs at: https://gpackage.io

## Installation
On Windows at least, use these commands to add the feed and install it
```
"C:\Program Files\National Instruments\NI Package Manager\nipkg.exe" feed-add --system --name=mgi-gpm https://s3-us-west-1.amazonaws.com/gpm-dist/master/
```
```
"C:\Program Files\National Instruments\NI Package Manager\NIPackageManager.exe" install gpm-windows --update-feeds
```

Use this command to setup the default.gpmrc file 
```
echo `
"@dsa:registry=folder://P:/cmh/gpm" `
"@dsa-actors:registry=folder://P:/cmh/gpm" `
> "~\.gpmrc"
```
or as a .bat file:
```
@echo off
(
    echo @dsa:registry=folder://P:/cmh/gpm
    echo @dsa-actors:registry=folder://P:/cmh/gpm
) > "%USERPROFILE%\.gpmrc"
```
