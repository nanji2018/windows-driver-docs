---
title: IrqlKeRaiseLower rule (wdm)
description: The IrqlKeRaiseLower rule specifies that the driver does the following when raising and lowering the IRQL When the driver calls KeRaiseIrql, it is executing at an IRQL that is lower than or equal to the value of the NewIrql parameter.The driver calls KeLowerIrql only after calling KeRaiseIrql or KeRaiseIrqlToDpcLevel.
ms.assetid: 61f7e5bc-ccc5-4ee6-a580-9935a01f96e6
keywords: ["IrqlKeRaiseLower rule (wdm)"]
topic_type:
- apiref
api_name:
- IrqlKeRaiseLower
api_type:
- NA
---

# IrqlKeRaiseLower rule (wdm)


The **IrqlKeRaiseLower** rule specifies that the driver does the following when raising and lowering the IRQL:

When the driver calls [**KeRaiseIrql**](https://msdn.microsoft.com/library/windows/hardware/ff553079), it is executing at an IRQL that is lower than or equal to the value of the *NewIrql* parameter.
The driver calls [**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968) only after calling **KeRaiseIrql** or [**KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084).
This rule permits nested calls to **KeRaiseIrql**, **KeRaiseIrqlToDpcLevel**, and **KeLowerIrql**.

|              |     |
|--------------|-----|
| Driver model | WDM |

How to test
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">At compile time</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Run [Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808) and specify the <strong>IrqlKeRaiseLower</strong> rule.</p>
Use the following steps to run an analysis of your code:
<ol>
<li>[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)</li>
<li>[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)</li>
<li>[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)</li>
</ol>
<p>For more information, see [Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281).</p></td>
</tr>
</tbody>
</table>

Applies to
----------

[**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)
[**KeRaiseIrql**](https://msdn.microsoft.com/library/windows/hardware/ff553079)
See also
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md)
[**IrqlKeRaiseLower2**](wdm-irqlkeraiselower2.md)
 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevtest\devtest%5D:%20IrqlKeRaiseLower%20rule%20%28wdm%29%20%20RELEASE:%20%281/17/2018%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




