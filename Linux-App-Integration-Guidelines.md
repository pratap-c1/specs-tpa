[<< Back to HOME](README.md)

# Linux App Integration Guidelines

## TPA app communication:

TPA app should implement following deeplinks commands:

|  Command	|   Characteristics	|
| :-- | :-- |
| `tpa://launch?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS linux app will inform the tpa app about CMS `deviceId` and the `timeoutInSeconds` to be used for implementing the idle logic on the tpa app. CMS will call this command when they want to launch the TPA app. |

TPA app should implement following api's:

|  API	|   Characteristics	|
| :-- | :-- |
| `http://localhost:3000/tpa-request?tpappId=<TPA-APP-ID>&tpaVersion=<TPA-VERSION>` | TPA app must be call this api for information sharing like - `deviceId`, `timeoutInSeconds` etc... |
| `http://localhost:3000/tpa-pause?tpappId=<TPA-APP-ID>` | TPA app must be call this api on launching. |
| `http://localhost:3000/tpa-resume` | TPA app must be call this api before closing. |
