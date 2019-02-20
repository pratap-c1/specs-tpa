<< Back to [HOME](README.md)

# Windows-App-Integration-Guidelines

## CMS app commands

CMS windows app is a UWP (Universal Windows Platform) app. It accepts following commands:

CMS windows app using protocol to listen to the commands. This ensures that the command is delivered by the Windos OS to the CMS app even if the CMS app is not running

Below are command supported by the CMS app

|  Command	|   What does it do	|
| :-- | :-- |
| `pds://pause?tpappId=<tpappId>` | Pauses the CMS app and prevents it from coming to foreground. We will provide the `tpappId` to you |
| `pds://resume` | Informs a paused CMS app that it can now come back to foreground when it wants to	|

## TPA app commands

TPA app should implement following deeplinks (protocol) based commands:

|  Command	|   What TPA app should do	|
| :-- | :-- |
| `tpa://info?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS app will inform the tpa app about CMS `deviceId` and the timeout to be used for implementing the idle logic on the tpa app. Please note this is not a launch command but it is just a info command so you need to accept the info and close your app. |
| `tpa://launch` | CMS will call this command when they want to launch the TPA app |
