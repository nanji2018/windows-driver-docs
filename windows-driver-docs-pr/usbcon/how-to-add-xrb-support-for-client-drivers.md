---
Description: This topic describes how a USB client driver can use Windows Driver Model (WDM) driver routines to allocate and format an URB before sending the request to the Microsoft-provided USB driver stack.
title: Allocating and Building URBs
author: windows-driver-content
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Allocating and Building URBs


This topic describes how a USB client driver can use Windows Driver Model (WDM) driver routines to allocate and format an URB before sending the request to the Microsoft-provided USB driver stack.

The client driver uses an URB to package all information required by the lower drivers in the USB driver stack to process the request. In the Windows operating system, an URB is described in a [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure.

Microsoft provides a library of [Routines for USB Client Drivers](https://msdn.microsoft.com/library/windows/hardware/ff540134#client). By using those routines, USB client drivers can build URB requests for certain specified operations and forward them down the USB stack. If you prefer, you can design your client driver to call the library routines for the supported operations rather than building your own URB requests.

This topic contains the following sections:

-   [URB Allocation in Windows 7 and Earlier](#urb-allocation-in-windows-7-and-earlier)
-   [URB Allocation in Windows 8](#urb-allocation-in-windows-8)
-   [URB Routine Migration](#urb-routine-migration)
-   [Related topics](#related-topics)

## URB Allocation in Windows 7 and Earlier


To send a USB request by using routines included in Windows Driver Kit (WDK) for Windows 7 and earlier versions of Windows, a client driver typically allocates and fills a [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure, associates the **URB** structure with a new IRP, and sends the IRP to the USB driver stack.

For certain types of requests, Microsoft provides helper routines (exported by Usbd.sys) that allocate and format the [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure. For example, the [**USBD\_CreateConfigurationRequestEx**](https://msdn.microsoft.com/library/windows/hardware/ff539029) routine allocates memory for an **URB** structure, formats the URB for a select-configuration request, and returns the address of the **URB** structure to the client driver. However, the helper routines cannot be used for all types of requests.

Microsoft also provides macros that format URBs for some types of requests. For those macros, the client driver must allocate the [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure by calling [**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520) or allocate the structure on the stack. For example, after the client driver allocates an **URB**, the driver can call [**UsbBuildSelectConfigurationRequest**](https://msdn.microsoft.com/library/windows/hardware/ff538968) to format the URB for a select-configuration request or to clear the configuration.

For other requests the client driver must allocate and format the URB manually by setting various members of the [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure, depending on the request type.

When a USB request is complete, the client driver must release the [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure. If the URB is allocated on the stack, the URB is released when it goes out of scope. If the URB is allocated in nonpaged pool, the client driver must call [**ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590) to release the URB.

## URB Allocation in Windows 8


WDK for Windows 8 provides a new static library, Usbdex.lib, that exports routines for allocating, formatting, and releasing URBs. In addition, there is a new way of associating an URB with an IRP. The new routines can be called by a client driver targeting Windows Vista and later versions of Windows.

A client driver running on Windows Vista and later must use the new routines so that the underlying USB driver stack can utilize certain performance and reliability improvements. Those improvements apply to the new USB driver stack introduced in Windows 8 to support USB 3.0 devices and host controllers. For USB 2.0 host controllers, Windows loads an earlier version of the driver stack that does not support the improvements. Regardless of the version of the underlying driver stack or the protocol version supported by the host controller, you must always call the new URB routines.

Before you call any of the new routines, make sure that you have a USBD handle for your client driver registration with the USB driver stack. To obtain a USBD handle, call [**USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241).

The following routines are available with the WDK for Windows 8. These routines are defined in Usbdlib.h.

-   [**USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)
-   [**USBD\_IsochUrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406231)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)
-   [**USBD\_UrbFree**](https://msdn.microsoft.com/library/windows/hardware/hh406252)
-   [**USBD\_AssignUrbToIoStackLocation**](https://msdn.microsoft.com/library/windows/hardware/hh406228)

The allocation routines in the preceding list return a pointer to a new [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure, which is allocated by the USB driver stack. Depending on the version of the USB driver stack loaded by Windows, the **URB** structure can be paired with an opaque *URB context*. An URB context is a block of information about the URB. You cannot view the contents of the URB header; the information is intended to be used internally by the USB driver stack to improve URB tracking and processing. The URB context is *only* used by the USB driver stack for Windows 8.
If URB context is available, the USB driver stack uses it to make URB processing safer and more efficient. For example, the USB driver stack must make sure that the client driver does not submit an URB and then attempt to reuse that same URB before the first request has completed. To detect that kind of error, the USB driver stack stores state information in the URB context. Without the state information, the USB driver stack would have to compare the incoming URB with all URBs currently in progress. The state information is also used by the USB driver stack when the client driver attempts to release the URB. Before releasing the URB, the USB driver stack verifies the state to make sure that the URB is not pending.

URB context provides an official mechanism for storing extra URB information. Using URB context is preferable to allocating extra memory as needed or storing extra information in reserved members of the [**URB**](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure. The USB driver stack allocates URBs and their associated URB context in nonpaged pool, so that in the future if larger URB context are needed, the only required adjustment will be the size of a pool allocation.

## URB Routine Migration


The following table summarizes the changes in URB routines.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Use case</th>
<th>Available in WDK for Windows 7 and earlier</th>
<th>Available in WDK for Windows 8</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td>Targets Windows 7 and earlier versions of the operating system</td>
<td>Targets Windows Vista and later versions of the operating system</td>
</tr>
<tr class="even">
<td>To create an URB...</td>
<td>The client driver allocates a [<strong>URB</strong>](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure and formats the structure depending on the request.
<p>The client driver allocates the URB structure on the stack, or the driver allocates the structure in nonpaged pool by calling [<strong>ExAllocatePoolWithTag</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544520).</p></td>
<td>The client driver calls [<strong>USBD_UrbAllocate</strong>](https://msdn.microsoft.com/library/windows/hardware/hh406250) and receives a pointer to the new [<strong>URB</strong>](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure, which is allocated by the USB driver stack. The URB might be associated with an URB context, depending on the USBD interface version of the underlying USB driver stack.</td>
</tr>
<tr class="odd">
<td>To create an URB for a select-configuration request...</td>
<td>The client driver calls the [<strong>USBD_CreateConfigurationRequestEx</strong>](https://msdn.microsoft.com/library/windows/hardware/ff539029) routine that returns a pointer to the new URB that is created and formatted by the USB driver stack.</td>
<td>The client driver calls [<strong>USBD_SelectConfigUrbAllocateAndBuild</strong>](https://msdn.microsoft.com/library/windows/hardware/hh406243) and receives a pointer to the new [<strong>URB</strong>](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure, which is allocated and formatted (for the select-configuration request) by the USB driver stack. The URB might be associated with an URB context, depending on the USBD interface version of the underlying USB driver stack.</td>
</tr>
<tr class="even">
<td>To create a URB for an select-interface request...</td>
<td>The client driver allocates a [<strong>URB</strong>](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure and uses the [<strong>_URB_SELECT_INTERFACE</strong>](https://msdn.microsoft.com/library/windows/hardware/ff540425) structure to define the format of a select interface command for a USB device.</td>
<td>The client driver calls [<strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong>](https://msdn.microsoft.com/library/windows/hardware/hh406245) and receives a pointer to the new [<strong>URB</strong>](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure, which is allocated and formatted (for the select-interface request) by the USB driver stack. The URB might be associated with an URB context, depending on the USBD interface version of the underlying USB driver stack.</td>
</tr>
<tr class="odd">
<td>To associate an URB with an IRP...</td>
<td>The client driver gets a pointer to the next IRP stack location by calling [<strong>IoGetNextIrpStackLocation</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549266). Then the client driver manually sets the <strong>Parameters.Others.Argument1</strong> member of the stack location to the address of the [<strong>URB</strong>](https://msdn.microsoft.com/library/windows/hardware/ff538923) structure.</td>
<td>The client driver gets a pointer to the next IRP stack location by calling [<strong>IoGetNextIrpStackLocation</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549266). Then the client driver calls [<strong>USBD_AssignUrbToIoStackLocation</strong>](https://msdn.microsoft.com/library/windows/hardware/hh406228) to associate a the URB with the stack location.</td>
</tr>
<tr class="even">
<td>To release an URB...</td>
<td>If the client driver allocates a URB on the stack, the variable goes out of scope after the request is complete.
<p>To free a URB structure that the client driver or the USB driver stack allocated in nonpaged pool, the client driver calls [<strong>ExFreePool</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544590).</p></td>
<td>The client driver calls [<strong>USBD_UrbFree</strong>](https://msdn.microsoft.com/library/windows/hardware/hh406252).</td>
</tr>
</tbody>
</table>

 

## Related topics
[Sending Requests to a USB Device](communicating-with-a-usb-device.md)  

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Busbcon\buses%5D:%20Allocating%20and%20Building%20URBs%20%20RELEASE:%20%281/26/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


