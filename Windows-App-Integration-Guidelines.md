[<< Back to HOME](README.md)

# Windows-App-Integration-Guidelines

## CMS app commands

CMS windows app is a UWP (Universal Windows Platform) app. It accepts following commands:

CMS windows app using protocol to listen to the commands. This ensures that the command is delivered by the Windos OS to the CMS app even if the CMS app is not running

Below are command supported by the CMS app

|  Command	|   What does it do	|
| :-- | :-- |
| `pds://pause?tpappId=<tpappId>` | Pauses the CMS app and prevents it from coming to foreground. We will provide the `tpappId` to you. Eg: `pds://pause?tpappId=13` |
| `pds://resume` | Informs a paused CMS app that it can now come back to foreground when it wants to	
| `pds://request?tpappId=<tpappId>&launch=<true\|false>` | Request the info from the PDS app. Once this request is received PDS app will call the `info` command or `launch` command on the TPA app, depending upon the value of `launch` = `true` or `false`. TPA app will provide the `tpappId`. Eg: `pds://request?tpappId=13&launch=true` |
| `pds://info?tpappId=<tpappId>&appVersion=<appVersion>` | Receive the info from the TPA app. As of now we only need the `appVersion`. Eg: `pds://info?tpappId=13&appVersion=1.0.54` |

## TPA app commands

TPA app should implement following deeplinks (protocol) based commands:

|  Command	|   What TPA app should do	|
| :-- | :-- |
| `tpa://info?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS app will inform the tpa app about CMS `deviceId` and the timeout to be used for implementing the idle logic on the tpa app. Please note this is not a launch command but it is just a info command so you need to accept the info and close your app. |
| `tpa://launch?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS app will inform the tpa app about CMS `deviceId` and the timeout to be used for implementing the idle logic on the tpa app. CMS will call this command when they want to launch the TPA app |
| `tpa://request` | PDS App will request info from TPA using this command. TPApp is supposed send their app version by calling the `pds://info` command |

<b>Note</b>: 
1. `tpa` keyword in the above mentioned commands are placeholders. They will be replaced by a relevant keyword and will be provided CMS team.
2. TPApp should be calling the `pds://info` command only when they are launched first time after install/upgrade and any time the CMS app calls the `tpa://request` command
3. TPApp should be calling the `pds://pause` command only when they are not launched by CMS app. Manual launch should be the only case for this. In case of TPApp launch by any remote app, command `pds://request?tpappId=<tpappId>&launch=true` should be sent to CMS App and then CMS App will launch TPApp.
