---
title: PKEY\_FX\_ModeEffectClsid
description: In Windows 8.1 and later, the PKEY\_FX\_ModeEffectClsid property key identifies the mode effect (MFX) supported by the driver. The driver developer should specify the list of supported processing modes that their driver supports.
ms.assetid: 0B15A817-5F49-45B6-AD82-95738C4FF59C
ms.author: windowsdriverdev
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# PKEY\_FX\_ModeEffectClsid


In Windows 8.1 and later, the **PKEY\_FX\_ModeEffectClsid** property key identifies the mode effect (MFX) supported by the driver. The driver developer should specify the list of supported processing modes that their driver supports.

The INF file property key instructs the audio endpoint builder to set the CLSIDs for endpoint APOs into the effects property store. This information is used to build the audio graph that will be used to inform upper level apps what effects are in place.

## <span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF File Sample


An INF file specifies settings for an audio mode effect in the add-registry section for that device. The following INF example shows the strings and add-registry section that loads the APO for a mode effect into the registry.

```
[Strings]
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
```

## <span id="related_topics"></span>Related topics


[Media-Class INF Extensions](media-class-inf-extensions.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio\audio]:%20PKEY_FX_ModeEffectClsid%20%20RELEASE:%20%2811/22/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





