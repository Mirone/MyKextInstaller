<p align="center">
  <img alt="MyKextInstaller" src="https://i.ibb.co/JFMXDWyC/My-Kext-Installer-Icon.png" width="200">
</p>
<h3 align="center">MyKextInstaller</h3>

**MyKextInstaller** is an application designed to simplify the manual installation of  **kernel extensions (kexts)**  on macOS. While initially created to restore audio on system versions where original support was removed (such as macOS Tahoe Beta 2), it has evolved into a versatile and practical solution for general kext management.

This application automates critical tasks like copying files to the appropriate directories, configuring permissions, and updating system caches. This eliminates the complexity of the manual process, reduces reliance on alternative tools, and gives users more autonomy over the kexts they wish to install.

---

### How to use MyKextInstaller to restore audio?

To restore audio on your macOS system using MyKextInstaller, follow these steps:

1.  **Download MyKextInstaller:**
    
    -   Download the [MyKextInstaller](https://github.com/Mirone/MyKextInstaller/releases/latest/download/MyKextInstaller.zip) file.
        
2.  **Download AppleHDA.kext:**
    
    -   Download  [AppleHDA](https://github.com/Mirone/MyKextInstaller/releases/latest/download/AppleHDA.zip). You can use the macOS Sequoia version or earlier versions.
       
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

## Opening App
> [!IMPORTANT]
> MyKextInstaller is **notarized by Apple**, which means it passes Gatekeeper checks and will open normally 
> without requiring additional permissions or Terminal commands.
