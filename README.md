# MyKextInstaller

**MyKextInstaller** is an application designed to simplify the manual installation of  **kernel extensions (kexts)**  on macOS. While initially created to restore audio on system versions where original support was removed (such as macOS Tahoe Beta 2), it has evolved into a versatile and practical solution for general kext management.

This application automates critical tasks like copying files to the appropriate directories, configuring permissions, and updating system caches. This eliminates the complexity of the manual process, reduces reliance on alternative tools, and gives users more autonomy over the kexts they wish to install.

----------

### How to use MyKextInstaller to restore audio?

To restore audio on your macOS system using MyKextInstaller, follow these steps:

1.  **Download MyKextInstaller:**
    
    -   Download the [MyKextInstaller](https://github.com/Mirone/MyKextInstaller/releases/latest/download/MyKextInstaller.zip) file.
        
2.  **Download AppleHDA.kext:**
    
    -   Download  [AppleHDA](https://github.com/Mirone/MyKextInstaller/releases/latest/download/AppleHDA.zip). You can use the macOS Sequoia version or earlier versions.
        
    -   Alternatively, you can find  `AppleHDA.kext`  at the following path:  `/Library/Developer/KDKs/KDK_26.0_25A5279m.kdk/System/Library/Extensions`.
        
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
    
    ## Opening App
> [!IMPORTANT]
> This step is necessary, because the app has not been notarized by Apple due to the membership fees of the    Apple Developer Program. "Apple could not verify 'MyKextInstaller.app' is free of malware"
> 
**"Move to Trash" when opening the application:**

1. Right click `MyKextInstaller.app`
2. Click "Open"
3. Click "Open" in the dialog box
        
    -   If the error persists, go to  **System Settings**  →  **Privacy & Security**, scroll down until you find the blocked application (in this case, MyKextInstaller), and click  **Open Anyway**.
        
-   **Run command in terminal:**
    
    -   Alternatively, you can run the following command in Terminal to remove the file's quarantine:
        
        Bash
        
        ```
        xattr -d com.apple.quarantine /path/to/file
        ```
        
        (Replace  `/path/to/file`  with the full path to **MyKextInstaller**.)
        

----------

We hope MyKextInstaller makes managing your kexts a much simpler task! If you have any questions or encounter issues, don't hesitate to seek help from the [community](https://www.insanelymac.com/forum/topic/361340-mykextinstaller/#comment-2836303).
