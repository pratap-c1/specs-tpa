[<< Back to HOME](README.md)

# Linux App Integration Guidelines

## CMS app communication:

API supported by the CMS app:

|  API	|   Characteristics	|
| :-- | :-- |
| `http://localhost:3000/tpa-pause?tpappId=<TPA-APP-ID>` | Pauses the CMS app and prevents it from coming to foreground. You need to provide the `tpappId` |
| `http://localhost:3000/tpa-resume` | Informs a paused CMS app that it can now come back to foreground. |
| `http://localhost:3000/tpa-request?tpappId=<TPA-APP-ID>&tpaVersion=<TPA-VERSION>` | Information sharing. (Request the info from the TPA app with `tpappId` and `tpaVersion` and Receive the info from the CMS app. As of now only the `deviceId` and `timeoutInSeconds`). |

## TPA app communication:

TPA app should implement following deeplinks commands:

|  Command	|   Characteristics	|
| :-- | :-- |
| `tpa://launch?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS linux app will inform the tpa app about CMS `deviceId` and the `timeoutInSeconds` to be used for implementing the idle logic on the tpa app. CMS will call this command when they want to launch the TPA app. |

TPA app should implement following api's:

|  API	|   Characteristics	|
| :-- | :-- |
| `http://localhost:3000/tpa-request?tpappId=<TPA-APP-ID>&tpaVersion=<TPA-VERSION>` | TPA app must be call this api for information sharing. (Request the info from the TPA app with `tpappId` and `tpaVersion` and Receive the info from the CMS app. As of now only the `deviceId` and `timeoutInSeconds`). |
| `http://localhost:3000/tpa-pause?tpappId=<TPA-APP-ID>` | TPA app must be call this api on launching. |
| `http://localhost:3000/tpa-resume` | TPA app must be call this api before closing. |

<b>Note</b>:
* `tpa` keyword in the above mentioned commands are placeholders. They will be replaced by a relevant keyword and will be provided CMS team.
* For information sharing use api `/tpa-request`.
* TPA app should be calling the `/tpa-pause` api only when they are not launched by CMS app.
* TPA app should be calling the `/tpa-resume` api every time before closing TAP app.
