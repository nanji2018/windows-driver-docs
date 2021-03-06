---
title: KSPROPSETID\_TopologyNode
description: KSPROPSETID\_TopologyNode
ms.assetid: 0b6696aa-e80d-4806-9fbb-7de701164877
keywords: ["KSPROPSETID_TopologyNode"]
ms.author: windowsdriverdev
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# KSPROPSETID\_TopologyNode


## <span id="ddk_kspropsetid_topologynode_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGYNODE_KS"></span>


The `KSPROPSETID_TopologyNode` property set provides generic control over the various topology nodes. For a list of topology node types, see [Audio Topology Nodes](audio-topology-nodes.md). The properties in this set can be used to enable, disable, and reset topology nodes.

To expose AEC (acoustic echo cancellation) hardware acceleration to the system, an audio driver must implement AEC and noise-suppression nodes ([**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md) and [**KSNODETYPE\_NOISE\_SUPPRESS**](ksnodetype-noise-suppress.md)), and must support enabling and disabling of these nodes through the `KSPROPSETID_TopologyNode` properties. For more information, see [Exposing Hardware-Accelerated Capture Effects](https://msdn.microsoft.com/library/windows/hardware/ff536379).

A [**KSNODETYPE\_PROLOGIC\_ENCODER**](ksnodetype-prologic-encoder.md) node must also support the `KSPROPSETID_TopologyNode` properties.

The `KSPROPSETID_TopologyNode` property set contains the following properties:

[**KSPROPERTY\_TOPOLOGYNODE\_ENABLE**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_RESET**](ksproperty-topologynode-reset.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio\audio]:%20KSPROPSETID_TopologyNode%20%20RELEASE:%20%2811/22/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




