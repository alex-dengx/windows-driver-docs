---
title: Implementation Overview
description: This topic is an overview of the implementation key points that you must be aware of, when you develop a driver for an audio adapter that is capable of processing hardware-offloaded audio streams.
ms.assetid: B93B9A6D-7317-482B-A0B8-298CE8F21193
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Implementation Overview


This topic is an overview of the implementation key points that you must be aware of, when you develop a driver for an audio adapter that is capable of processing hardware-offloaded audio streams.

## <span id="The_New_KS_Filter_Topology"></span><span id="the_new_ks_filter_topology"></span><span id="THE_NEW_KS_FILTER_TOPOLOGY"></span>The New KS Filter Topology


In Windows 8 and later operating systems, support has been provided for a new type of audio adapter that can use an on-board hardware audio engine to process audio streams. When you develop such an audio adapter, the associated audio driver must expose this fact to the user mode audio system in a specific manner, so that the audio system can discover, use and properly expose the features of this adapter and its driver.

To make it possible for audio drivers to expose the hardware capabilities of these new audio adapters, Windows 8 introduces a new KS-filter topology that the driver must use:

![the new ks-filter topology, showing a host process input pin, an offloaded audio input pin, and a loopback output pin. audio processing is applied to the audio streams from the offloaded audio and host process pins.the loopback path is taken from the output of the final processing stage and leads directly out of the ks-filter topology. the other two streams flow through the dac and out of the ks-filter topology.](images/audio-engine-ksftopology.png)

As you can see in the preceding figure, a KS-filter topology represents the data paths through the hardware, and also shows the functions that are available on those paths. In the case of an audio adapter that can process offloaded audio, there are the following inputs and outputs (called pins) on the KS-filter:

-   One Host Process pin. This represents the input into the KS-filter from the software audio engine.

-   One Loopback pin. This represents an output from the hardware audio engine to the Windows audio session API (WASAPI) layer.

-   A number of Offloaded-audio pins. Although the figure shows only one pin of this type, an IHV is free to implement any number (n) of pins.

For more information about the pins in this new type of KS-filter topology, see [Architectural Overview](architectural-overview.md).
The actual service in the user mode audio system that "leads" to the discovery of the audio adapter and its driver, is the AudioEndpointBuilder. The AudioEndpointBuilder service monitors the **KSCATEGORY\_AUDIO** class for device interface arrivals and removals. When an audio device driver registers a new instance of the **KSCATEGORY\_AUDIO** device interface class, a device interface arrival notification is fired off. The AudioEndpointBuilder service detects the device interface arrival notification and uses an algorithm to examine the topology of the audio devices in the system so that it can take appropriate action.

So when you develop your audio driver to support an adapter that is capable of processing offloaded-audio, your driver must use the newly-defined [**KSNODETYPE\_AUDIO\_ENGINE**](https://msdn.microsoft.com/library/windows/hardware/hh450866) audio endpoint to expose the capabilities of the hardware audio engine. For more information about the audio endpoint discovery process, see [Audio Endpoint Builder Algorithm](audio-endpoint-builder-algorithm.md).

## <span id="User_Interface_Considerations"></span><span id="user_interface_considerations"></span><span id="USER_INTERFACE_CONSIDERATIONS"></span>User Interface Considerations


You developed your audio driver to control the underlying hardware capabilities of an audio adapter that is capable of processing offloaded-audio. This means that your driver has the best knowledge about how to control the adapter's features. So you must develop a UI that will expose the features of the adapter to the end user in the form of options that they can select, enable and/or disable.

If however, you already have a UI that is used for controlling audio processing objects (APOs) that you developed, this UI could be extended to work with your new audio adapter. In this case, your extensions to the UI would provide software control for the APOs, and hardware control for the adapter.

## <span id="Application_Impact"></span><span id="application_impact"></span><span id="APPLICATION_IMPACT"></span>Application Impact


The functionality described for this new type of audio adapter and its associated driver, can be used by Windows Store apps via WASAPI, Media Foundation, Media Engine, or the HTML 5 &lt;audio&gt; tags. Note that Wave and DSound cannot be used, as they are not available to Windows Store apps. Also note that Desktop applications cannot use the offloading capabilities of audio adapters that support hardware-offloaded audio. These applications can still render audio, but only through the host pin which makes use of the software audio engine.

If a Windows Store app streams media content and uses Media Foundation, Media Engine, or the HTML 5 &lt;audio&gt; tags, the app is automatically opted-in for hardware offloading as long as the proper audio category has been set for the stream. Opting-in for hardware offloading is done on a per stream basis.

Windows Store apps that use WASAPI or streaming communications have to explicitly opt-in for hardware offloading.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio\audio]:%20Implementation%20Overview%20%20RELEASE:%20%287/18/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


