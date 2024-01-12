# AntiAntiDefraud

Prevent MIUI from uploading your privacy data.

---

## How does MIUI collect your privacy?

Since version 14 upgrade, MIUI starts to send UUID from `GuardProvider`, MIUI version, installed apps among other information to Xiaomi's server without user's knowledge.

MIUI Chinese version has been confirmed to collect these data through `AntiDefraud`. **This is also found in the global version**.

Certain behaviours have been found to trigger data uploading:
* Go to `Security` - `Settings` - `Security scan`, `Check for updates` (regardless of `Online definitions` option)
* Force stop `SecurityCenter` (regardless of `Online definitions` option)
* Clear data of `Security` in `Applications`

## How does AntiAntiFraud protect you?

This XPosed module configures `GuardProvider` into debug mode. With that, MIUI no longer uploads your data. This also enables logging function which can be viewed in LSPosed later.

To do this, install the module, then activate in LSPosed.

## Log messages

### Info: GuardProvider will work as debug mode!

This indicates `GuardProvider` have been successfully configured into debug mode. You can safely ignore the subsequent `Warning: GuardProvider debug mode flag not found!`.

From this message on, logs will be printed if `GuardProvider` request is intercepted.

### W/TAG: responseDetectApp get: {"code":200,"desc":"success","data":[]}

This message can be found in `logcat` (not LSPosed's `Log`). This is normal, as the module has blocked `GuardProvider` from actually sending anything.

### Skip: AntiDefraudAppManager class not found.
### Skip: getAllUnSystemAppsStatus method not found.
These two messages indicate failure in finding `GuardProvider` and the module isn't working as expected.

Check your MIUI version. If you're using versions lower than 14, you don't need `AntiAntiFraud`.

If not, this is probably bacause you're using an incompatible version. Please report this to issues.

### Info: Intercept={"timestamp":"xxx","os":"xxx","biz_id":"virus_scan","uuid":"xxx","content":[]}
This shows actual data upload requests from `GuardProvider`. This is what MIUI wants to collect. The request won't be uploaded, so you can safely ignore this message.

### Warning: Can't get MIUI_VERSION.  
### Warning: uuidHelper class not found.  
### Warning: getUUID method not found.  
### Info: xxxxxx
You can safely ignore these messages.
