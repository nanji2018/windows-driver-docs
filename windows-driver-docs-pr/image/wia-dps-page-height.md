---
title: WIA\_DPS\_PAGE\_HEIGHT
description: The WIA\_DPS\_PAGE\_HEIGHT property contains the height, in thousandths of an inch (.001), of the currently selected page. The WIA minidriver creates and maintains this property.
ms.assetid: 93970d9a-96fe-4cf9-98c6-4ddcfd425214
keywords: ["WIA_DPS_PAGE_HEIGHT Imaging Devices"]
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.author: windowsdriverdev
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# WIA\_DPS\_PAGE\_HEIGHT


The WIA\_DPS\_PAGE\_HEIGHT property contains the height, in thousandths of an inch (.001), of the currently selected page. The WIA minidriver creates and maintains this property.

## <span id="ddk_wia_dps_page_height_si"></span><span id="DDK_WIA_DPS_PAGE_HEIGHT_SI"></span>


Property Type: VT\_I4

Valid Values: WIA\_PROP\_NONE

Access Rights: Read-only

Remarks
-------

An application reads WIA\_DPS\_PAGE\_HEIGHT to determine the physical dimensions of the page that is being scanned. If the extent settings are different from the known page sizes, this property reports the height of the page whose [**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md) property is set to WIA\_PAGE\_CUSTOM (which is a value of the WIA\_DPS\_PAGE\_SIZE property).

WIA\_DPS\_PAGE\_HEIGHT must provide a measurement in thousandths of an inch that is equivalent to the pixel value reported by the [**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md) property, which reports the height, in pixels, of the page to be scanned.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Available for Microsoft Windows XP. For Windows Vista and later, use the identical WIA_IPS_PAGE_HEIGHT property.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (include Wiadef.h)</td>
</tr>
</tbody>
</table>

## <span id="see_also"></span>See also


[**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md)

[**WIA\_DPS\_PAGE\_WIDTH**](wia-dps-page-width.md)

[**WIA\_IPS\_PAGE\_HEIGHT**](wia-ips-page-height.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bimage\image%5D:%20WIA_DPS_PAGE_HEIGHT%20%20RELEASE:%20%2811/13/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





