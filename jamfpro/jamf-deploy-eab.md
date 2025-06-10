# Mammoth Browser for iOS deployment guide for Jamf Pro

## General Requirements

Mammoth Browser is an enterprise browser. Your organization needs a browser management account from Mammoth Cyber in order to manage your users, browsers and devices. If you have any questions, please contact our sales or support. The rest of the document will focus on deploying the browser for your users.

> **Note:** Mammoth Browser is supported on iOS 17 or later. The latest version of the Mammoth Browser is available in the App Store.

> **Note:** It is recommended to utilize Volume Purchasing. You must have uploaded your volume purchasing token to Jamf Pro in order to use it.

## Install Mammoth Browser for iOS


1. In Jamf Pro, click **Devices** in the sidebar. Then select **Mobile Device Apps** option. On this page, click the **+New** button.
1. In the "Choose Type" page, select **App Store app or apps purchased in volume** as the type, then click the **Next** button.
1. In the "Search or upload" page, fill in **"mammoth browser"** as the App Store search phrase. The quote marks in the search phrase allow exact match. Click **Next** to show the search result page.
1. In the search result page, click the **Add** button next to the **Mammoth Browser** app to continue.
1. Then you will see the configuration options for the Mammoth Browser. A few options worth considering:
   * General -> Distribution Method -> Install Automatically/Prompt Users to Install
   * General -> Distribution Method -> Convert unmanaged app to managed
   * General -> Distribution Method -> Remove app when MDM profile is removed
   * General -> Distribution Method -> Prevent backup of app data
   * Managed distribution -> Device Assignments -> Assign Content Purchased in Volume (if you have imported a VPP token)
1. Click the **Scope** tab and configure the scope of the app.
1. On the **App Configuration** tab, add the following lines to the **Preferences** field.

    **Note: replace the placeholder "my-subdomain" with your real value**:

    ```xml
    <dict>
        <key>CustomDomain</key>
        <string>my-subdomain</string>
        <key>AutoLogin</key>
        <string>true</string>
        <key>UserDisplayName</key>
        <string>$FULLNAME</string>
        <key>UserName</key>
        <string>$USERNAME</string>
        <key>EmailAddress</key>
        <string>$EMAIL</string>
        <key>DeviceName</key>
        <string>$DEVICENAME</string>
        <key>UDID</key>
        <string>$UDID</string>
        <key>JAMF_MGMT_ID</key>
        <string>$MANAGEMENTID</string>
        <key>JSSID</key>
        <string>$JSSID</string>
        <key>Loc.Site</key>
        <string>$SITENAME</string>
        <key>Loc.Department</key>
        <string>$DEPARTMENTNAME</string>
        <key>Loc.Building</key>
        <string>$BUILDINGNAME</string>
        <key>Loc.Room</key>
        <string>$ROOM</string>
    </dict>
    ```
    * CustomDomain: The value is the custom subdomain of your account. If specified, users cannot use other subdomains to login.
    * AutoLogin: The value is true/false in string format. If a valid CustomDomain is provided and AutoLogin is "true", the browser will try to bring up the IdP's login page automatically.
    * UserName/EmailAddress: When these fields are specified, only a matching user is allowed to use the browser. The UserName value has higher priority over the EmailAddress value if both are available.

1. Click **Save**.

Mammoth Browser is distributed to mobile devices in the scope the next time they check in with Jamf Pro.

## End User Experience

If you did not enable "Assign Content Purchased in Volume", users may be prompted to enter an Apple Account before Mammoth Browser installs on their device.
