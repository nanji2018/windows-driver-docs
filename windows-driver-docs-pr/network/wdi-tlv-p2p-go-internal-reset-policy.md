---
title: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY
author: windows-driver-content
description: WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY is a TLV that contains the policy used by the firmware for operating channel selection after a Wi-Fi Direct GO Reset is stopped/restarted.
ms.assetid: 6EA61C65-8573-491D-9268-8A02440A1175
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY Network Drivers Starting with Windows Vista
---

# WDI\_TLV\_P2P\_GO\_INTERNAL\_RESET\_POLICY


WDI\_TLV\_P2P\_GO\_INTERNAL\_RESET\_POLICY is a TLV that contains the policy used by the firmware for operating channel selection after a Wi-Fi Direct GO Reset is stopped/restarted.

## TLV Type


0xB2

## Length


The size (in bytes) of a UINT32.

## Values


| Type                                                                                            | Description                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_GO\_INTERNAL\_RESET\_POLICY**](https://msdn.microsoft.com/library/windows/hardware/dn926096) (UINT32) | If an Wi-Fi Direct GO Reset is stopped/restarted by the IHV component on its own (for example, for Bluetooth co-ex spatial stream downgrade), this configuration defines the policy to be adopted by the firmware for operating channel selection after the reset. |

 

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Minimum supported client</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>Minimum supported server</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


