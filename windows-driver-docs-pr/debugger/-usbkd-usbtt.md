---
title: usbkd.usbtt
description: The usbkd.usbtt command displays information from a USBPORT \_TRANSACTION\_TRANSLATOR structure.
ms.assetid: 4D599BCE-C6C3-42B3-BDCE-EE9E47FA6AB7
keywords: ["usbkd.usbtt Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- usbkd.usbtt
api_type:
- NA
---

# !usbkd.usbtt


The **!usbkd.usbtt** command displays information from a **USBPORT!\_TRANSACTION\_TRANSLATOR** structure.

```
!usbkd.usbtt StructAddr
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
Address of a **usbport!\_TRANSACTION\_TRANSLATOR** structure. To get the transaction translator list for a USB host controller, use the [**!usbkd.usbhcdext**](-usbkd-usbhcdext.md) command.

## <span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

Examples
--------

Here is one way to find the address of a **usbport!\_TRANSACTION\_TRANSLATOR** structure. First enter [**!usbkd.usb2tree**](-usbkd-usb2tree.md).

```
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

In the preceding output, the address of the device extension of the FDO is displayed as the argument of the [DML](debugger-markup-language-commands.md) command **!ehci\_info ffffe00001ca11a0**.

Either click the DML command or pass the address of the device extension to [**!usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072) to get the address of `GlobalTtListHead`. Pass that address to [**!usbkd.usblist**](-usbkd-usblist.md), which will display addresses of **\_TRANSACTION\_TRANSLATOR** structures.

## <span id="see_also"></span>See also


[USB 2.0 Debugger Extensions](usb-2-0-extensions.md)

[Universal Serial Bus (USB) Drivers](http://go.microsoft.com/fwlink/p?LinkID=227351)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!usbkd.usbtt%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





