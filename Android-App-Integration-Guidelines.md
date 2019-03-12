<< Back to [HOME](README.md)

# Android App Integration Guidelines

## CMS app commands

CMS app needs to implement a [`BroadcastReceiver`](https://developer.android.com/reference/android/content/BroadcastReceiver) with following `actions` and read `extras`.

This `BroadcastReceiver` should listent to these `actions` as mentioned in table below

|  `val action = intent.action`	(commands) |   What does it do	|
| :-- | :-- |
| `PAUSE` | Pauses the CMS app and prevents it from coming to foreground. TP app should provide `tpappId` as a `Long` `extra` in then intent. Eg: `intent.putExtra(EXTRA_TPAPP_ID, 14L)` |
| `RESUME` | Informs a paused CMS app that it can now come back to foreground when it wants to. 
| `REQUEST` | Request the info from the PDS app. TP app should provide `tpappId` as a `Long` `extra` in then intent. TP app should also provide `launch` as a `boolean` extra. Depending upon the value of `launch` = `true` or `false` PDS app will broadcast the `launch` or `info` command. |

Smaple code snippet:
```kotlin
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.util.Log

const val PAUSE = "PAUSE"
const val RESUME = "RESUME"
const val REQUEST = "REQUEST"

const val EXTRA_TPAPP_ID = "EXTRA_TPAPP_ID"
const val EXTRA_LAUNCH = "EXTRA_LAUNCH"

class CommandsReceiver : BroadcastReceiver() {
    private val TAG = CommandsReceiver::class.java.canonicalName

    override fun onReceive(context: Context?, intent: Intent?) {
        if (intent != null) {
            val action: String? = intent.action
            val tpAppId: Long? = if (intent.hasExtra(EXTRA_TPAPP_ID)) {
                intent.getLongExtra(EXTRA_TPAPP_ID, -1L)
            } else {
                null
            }
            val launch: Boolean? = if (intent.hasExtra(EXTRA_LAUNCH)) {
                intent.getBooleanExtra(EXTRA_LAUNCH, false)
            } else {
                null
            }
            when (action) {
                PAUSE -> pauseApp(tpAppId)
                RESUME -> resumeApp()
                REQUEST -> handleRequest(tpAppId, launch)
            }
        }
    }

    fun pauseApp(tpAppId: Long?) {
        if (tpAppId == null) {
            Log.e(TAG, "tpAppId should not be null")
            return
        }
        TODO()
    }

    fun resumeApp() {
        TODO()
    }

    fun handleRequest(tpAppId: Long?, launch: Boolean?) {
        if (tpAppId == null) {
            Log.e(TAG, "tpAppId should not be null")
            return
        }
        if (launch == null) {
            Log.e(TAG, "launch should not be null")
            return
        }
        TODO()
    }
}
```

## TPA app commands

TPA app needs to implement a [`BroadcastReceiver`](https://developer.android.com/reference/android/content/BroadcastReceiver) with following `actions` and read `extras`.

This `BroadcastReceiver` should listent to these `actions` as mentioned in table below

| `val action = intent.action` (commands) |  What TPA app should do	|
| :-- | :-- |
| `tpa://info?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS app will inform the tpa app about CMS `deviceId` and the timeout to be used for implementing the idle logic on the tpa app. Please note this is not a launch command but it is just a info command so you need to accept the info and close your app. |
| `tpa://launch?deviceId=<deviceId>&timeoutInSeconds=<timeout>` | CMS app will inform the tpa app about CMS `deviceId` and the timeout to be used for implementing the idle logic on the tpa app. CMS will call this command when they want to launch the TPA app |

Sample code snippet:

```kotlin
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.util.Log


const val INFO = "INFO"
const val LAUNCH = "LAUNCH"

const val EXTRA_DEVICE_ID = "EXTRA_DEVICE_ID"
const val EXTRA_TIMEOUT_IN_SECONDS = "EXTRA_TIMEOUT_IN_SECONDS"

class CommandsReceiver : BroadcastReceiver() {
    private val TAG = CommandsReceiver::class.java.canonicalName

    override fun onReceive(context: Context?, intent: Intent?) {
        if (intent != null) {
            val action: String? = intent.action
            val deviceId: Long? = if (intent.hasExtra(EXTRA_DEVICE_ID)) {
                intent.getLongExtra(EXTRA_DEVICE_ID, -1L)
            } else {
                null
            }
            val timeoutInSeconds: Long? = if (intent.hasExtra(EXTRA_TIMEOUT_IN_SECONDS)) {
                intent.getLongExtra(EXTRA_TIMEOUT_IN_SECONDS, -1L)
            } else {
                null
            }
            when (action) {
                INFO -> saveInfo(deviceId, timeoutInSeconds)
                LAUNCH -> launchMyApp(deviceId, timeoutInSeconds)
            }
        }
    }

    fun saveInfo(deviceId: Long?, timeoutInSeconds: Long?) {
        if (deviceId == null) {
            Log.e(TAG, "deviceId should not be null")
            return
        }
        if (timeoutInSeconds == null) {
            Log.e(TAG, "timeoutInSeconds should not be null")
            return
        }
        TODO()
    }

    fun launchMyApp(deviceId: Long?, timeoutInSeconds: Long?) {
        if (deviceId == null) {
            Log.e(TAG, "deviceId should not be null")
            return
        }
        if (timeoutInSeconds == null) {
            Log.e(TAG, "timeoutInSeconds should not be null")
            return
        }
        TODO()
    }

}
```

