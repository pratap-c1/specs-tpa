[<< Back to HOME](README.md)

# Linux App Integration Guidelines

## TPA app communication:

TPA app should implement following deeplinks commands:

|  Command	|   Characteristics	|
| :-- | :-- |
| `tpa://launch?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS linux app will inform the tpa app about CMS `deviceId` and the `timeoutInSeconds` to be used for implementing the idle logic on the tpa app. CMS will call this command when they want to launch the TPA app |
