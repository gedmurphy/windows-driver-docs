---
title: 32-Bit and 64-Bit WIA Interoperability
author: windows-driver-content
description: 32-Bit and 64-Bit WIA Interoperability
MS-HAID:
- 'WIA\_Fundamentals\_60dec3ad-c926-4a31-bc65-60d5fda6b6bf.xml'
- 'image.32\_bit\_and\_64\_bit\_wia\_interoperability'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: f7f7a42a-590e-4f81-b325-ba9f9ffa9664
---

# 32-Bit and 64-Bit WIA Interoperability


On systems that run Windows 64-Bit Edition for Extended Processors, all WIA components are 64-bit so the WIA infrastructure was changed to allow interoperability between these 64-bit drivers and existing 32-bit applications.

On 64-bit editions of the Windows operating system, the 64-bit WIA minidriver is loaded in the WIA service's 64-bit process. However, WIA minidriver UI extensions are loaded in the application's process space. A Microsoft Win32 application's unmodified 32-bit process that runs on an x64-based machine would not be able to load the 64-bit UI extension.

To mitigate the 32-bit to 64-bit problem, Microsoft provides a 64-bit extension host, *wiawow64.exe*. This host ensures transparent interoperability between 32-bit applications and 64-bit WIA UI extensions. The *wiawow64.exe* extension host will be available in Windows Server 2003 64-Bit Edition for Extended Processors, Windows XP 64-Bit Edition for Extended Processors, Windows Vista, and later operating system versions.

The WIA service will determine where UI extensions get physically loaded, depending on whether the application is 64-bit or 32-bit:

-   *64-bit application*. The 64-bit WIA minidriver UI extension is loaded directly into the process space of the application. This is similar to what happens when you run a 32-bit application on 32-bit versions of the Windows operating system.

-   *32-bit application*. WIA launches the *wiawow64.exe* extension host that UI extensions will be loaded into. A separate instance of *wiawow64.exe* is created and launched each time a call to any of the interface methods comes in from a 32-bit application. The *wiawow64.exe* host runs in the same context as the application and communicates with the application through the existing COM interfaces.

    **Note**   Even though *wiawow64.exe* is completely transparent to both WIA application writers and WIA driver developers, driver developers have to debug the *wiawow64.exe* process rather than the 32-bit application to debug 64-bit UI extensions.

     

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bimage\image%5D:%2032-Bit%20and%2064-Bit%20WIA%20Interoperability%20%20RELEASE:%20%288/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

