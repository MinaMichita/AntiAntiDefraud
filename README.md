# AntiAntiDefraud

Preventing Miui from uploading installed app list.

---

## How Miui collect your privacy?

Since Miui 14, Miui is keeping sending information that contain uuid from GuardProvider, Miui version and installed app information list to Xiaomi's server without asking user.

Miui China Mainland version has been tested and confirmed that Xiaomi is collecting user's privacy without asking their users. Xiaomi named this function as AntiDefraud in their code and **these code is also existing in Miui Global version**.

Behavior list below will trigger Miui to uploading your installed app list(Tested on Miui China Mainland version):
* Launch Security - Settings - Security scan - Check for updates(Whether Online definitions is on or off)
* Force Stop SecurityCenter(Whether Online definitions is on or off)
* Clear Security app data

## What will this xposed module do?

This xposed module will make GuardProvider work as debug mode and preventing Miui from uploading installed app list and print log with content that Miui want to collect.

Install this app and active it in lsposed. You can check log in lsposed to confirm is Miui uploading your installed app list.

### About Debug mode flag process log

**Info: GuardProvider will work as debug mode!**  
That means GuardProvider is working as debug mode and it will print log if GuardProvider is sending your installed app list to Xiaomi's server. Besides, if this appear, you can ignore **Warning: GuardProvider debug mode flag not found!**.  
You can do a research in logcat(not in lsposed) with keyword **responseDetectApp**, and then you can find log:  
*W/TAG: responseDetectApp get: {"code":200,"desc":"success","data":[]}*  
But if this xposed module work correctly, the above log can not be found is normal cause this module will prevent Miui from uploading installed app list.

**Info: GuardProvider will work as debug mode!**  
GuardProvider will not work as debug mode and this means GuardProvider will not print log when it uploads your installed app list.

### About Prevent miui from uploading app list log

**Skip: AntiDefraudAppManager class not found.**  
**Skip: getAllUnSystemAppsStatus method not found.**  
That means this module can't find the code will upload your installed app list. It is normal if you are not using Miui 14.  
But If you are using Miui 14, maybe Xiaomi has edited the code. Maybe Xiaomi has deleted or just renamed to make this module not to work.

**Info: Intercept={"timestamp":"xxx","os":"xxx","biz_id":"virus_scan","uuid":"xxx","content":[]}**  
That means Miui is trying to upload your installed app list to Xiaomi's server but this module intercepted it. You can check it to know which information is collecting by Xiaomi.

**You can ignore these log:**  
Warning: Can't get MIUI_VERSION.  
Warning: uuidHelper class not found.  
Warning: getUUID method not found.  
Info: xxxxxx