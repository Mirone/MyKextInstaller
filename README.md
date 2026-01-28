<p align="center">
  <img alt="MyKextInstaller" src="https://i.ibb.co/JFMXDWyC/My-Kext-Installer-Icon.png" width="200">
</p>
<h3 align="center">MyKextInstaller</h3>

**MyKextInstaller** is an application designed to simplify the manual installation of  **kernel extensions (kexts)**  on macOS. While initially created to restore audio on system versions where original support was removed (such as macOS Tahoe Beta 2), it has evolved into a versatile and practical solution for general kext management.

This application automates critical tasks like copying files to the appropriate directories, configuring permissions, and updating system caches. This eliminates the complexity of the manual process, reduces reliance on alternative tools, and gives users more autonomy over the kexts they wish to install.

[Support this project](https://www.paypal.com/donate/?cmd=_s-xclick&hosted_button_id=K4M7MJFLXUU6Y&ssrt=1753621430494)

---

### How to use MyKextInstaller to restore audio?

To restore audio on your macOS system using MyKextInstaller, follow these steps:

1.  **Download MyKextInstaller:**
    
    -   Download the [MyKextInstaller](https://github.com/Mirone/MyKextInstaller/releases/latest/download/MyKextInstaller.zip) file.
        
2.  **Download AppleHDA.kext:**
    
    -   Download  [AppleHDA](https://github.com/Mirone/MyKextInstaller/releases/latest/download/AppleHDA.kext.zip). You can use the macOS Sequoia version or earlier versions.
       
    -   Alternatively, you can find  `AppleHDA.kext`  at the following path:  `/Library/Developer/KDKs/KDK_26.0_25A5279m.kdk/System/Library/Extensions`.
    
> [!TIP]
> Starting from version 1.4 of MyKextInstaller, the AppleHDA kext is installed automatically.
>         
3.  **Configure SIP (System Integrity Protection):**
    
    -   **For OpenCore users:**  Set  `csr-active-config=03080000`  in your  `config.plist`. If you need help, check [here](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/extended/post-issues.html#disabling-sip).
        
    -   **For Clover users:**  Set  `CsrActiveConfig=0x803`  in your  `config.plist`. If you need help, check [here](https://github.com/CloverHackyColor/Clover-Documentation?tab=readme-ov-file#csractiveconfig).
        
4.  **Verify AppleALC.kext:**
    
    -   Make sure  `AppleALC.kext`  is enabled in the  `Kernel`  section of your  `config.plist`  in OpenCore, as it was before. If you don't know how, check [here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/#config-plist-setup%5D(https://dortania.github.io/OpenCore-Install-Guide/config.plist/%23config-plist-setup)).
        
5.  **Download and install the KDK (Kernel Development Kit):**
    
    -   Install the appropriate [KDK](https://github.com/dortania/KdkSupportPkg/releases) for your macOS version.
        
6.  **Install AppleHDA.kext with MyKextInstaller:**
    
    -   Open MyKextInstaller. The application will ask you to locate the kext you want to install. For convenience, copy  `AppleHDA.kext`  to your Desktop.
        
7.  **Restart your system:**
    
    -   After installing the kext, restart your system and check if the audio is working correctly.
        

----------

### Common troubleshooting

-   Any instructions related to disabling SIP in Recovery Mode apply to systems where SIP is still enabled in  `config.plist`.

---

### Security

**MyKextInstaller** uses a Helper Tool to perform tasks that require elevated privileges (root).

* **Versions 1.4 to 1.6**: The helper was installed using **SMJobBless**, ensuring compatibility with earlier versions of macOS such as Big Sur and Monterey.
* **Starting with version 1.7**: It began using the **SMAppService** API, the modern approach recommended by Apple for managing auxiliary services.
    * This migration aligns the application with the security architecture of **macOS 13 Ventura** or later.

---

### Is it safe to use a Helper Tool?

**Yes**, when it is part of a trustworthy application.  
**MyKextInstaller** meets the main security requirements defined by Apple:

* It uses an official Apple API (**SMAppService**).
* The **Helper Tool** is signed with the same **Developer ID** as the main application.
* The App is **notarized by Apple**.
* Installation and execution of the helper are controlled by **macOS (launchd)**.
* The **Helper Tool** can only be installed with **explicit user authorization**.
* The execution scope of the helper is limited to the tasks defined by the application.

---

### Helper Tool scope

The Helper Tool is used exclusively to perform operations that require elevated privileges, such as:

* Kext installation
* Kext removal
* Rebuilding system caches
* Restoring system snapshots
* Mounting partitions

> [!IMPORTANT]
> The Helper Tool is **not authorized nor implemented** to perform any task outside the scope of MyKextInstaller.

---

### Can the Helper Tool spy on the user or perform malicious actions?

Technically, any software can be malicious. However:

* Using **SMAppService** does not grant extra privileges by itself.
* It does not bypass macOS security mechanisms.
* The helper does not have automatic access to user data.
* Any sensitive action remains subject to system security policies.

---

### How it works in practice?

* **SMAppService** registers a Helper Tool (Launch Daemon) with the system.
* This helper is installed with elevated privileges (root), but it can only be started when requested by the main application (MyKextInstaller).
* **launchd** manages the execution of the helper, ensuring it runs on demand and within the authorized scope.
* The helper does not remain active all the time. It only runs when needed.

---

### Why does SMJobBless show the developer name in system notifications while SMAppService shows the app name?

#### SMJobBless
* **Context**: It was the legacy API used to install Privileged Helper Tools.
* **Displayed identity**: In system notifications, the **developer name** associated with the Developer ID was shown.
* **Reason**: The focus was on ensuring the tool was signed by a verified developer. The system highlighted the legal entity responsible for the code.
  * **Message displayed by SMJobBless**:
	  - Background app activity
The software from “Developer Name” can be run in the background. Manage background activity in Login Items and Extensions.

#### SMAppService
* **Context**: It is the modern API that replaces SMJobBless for service registration.
* **Displayed identity**: System notifications now show the **application name** requesting the service.
* **Reason**: Apple shifted to an app-centric user experience.
    * Users recognize the **app** they are interacting with more easily than the developer's registered name.
    * This makes messages clearer for example: 
    * **Message displayed by SMAppService**:
		- Background app activity
The MyKextInstaller app can run in the background for all users.
Do you want to allow this?
    * The link to the Developer ID remains active for internal validation, but the UI prioritizes the app's identity.

### In summary

- When using **SMJobBless**, the system displays a prompt asking for the user’s password to install the *Helper Tool*.  
- Once the installation is authorized, the application is automatically added to **System Settings > Login Items**, becoming enabled without any further action required.  
- With **SMAppService**, however, after installation the application is **not automatically enabled** in the Login Items. In this case, **the user must activate it manually.**  


---

### Apple Developer Documentation

* **Service Management Framework** – [Overview of the framework](https://developer.apple.com/documentation/servicemanagement)
* **SMJobBless** – [Legacy function for privileged helpers](https://developer.apple.com/documentation/servicemanagement/smjobbless%28_%3A_%3A_%3A_%3A%29)
* **SMAppService** – [Modern API for service registration](https://developer.apple.com/documentation/servicemanagement/smappservice)
* **Migration Guide** – [Updating to the New Service Management API](https://developer.apple.com/documentation/ServiceManagement/updating-your-app-package-installer-to-use-the-new-service-management-api)
