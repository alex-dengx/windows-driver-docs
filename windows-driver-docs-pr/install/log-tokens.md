---
title: Log Tokens
description: Log Tokens
ms.assetid: f666d457-eb0a-4482-a8ac-e2921ab8c5a9
keywords:
- log tokens WDK SetupAPI
- text logs WDK SetupAPI , log tokens
- sections WDK SetupAPI logging
- identifying text log sections
- SetupAPI logging WDK Windows Vista , log tokens
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Log Tokens


SetupAPI text logging uses *log tokens* to write entries in a [SetupAPI text log](setupapi-text-logs.md).

A class installer or co-installer must use the log token that is returned by [**SetupGetThreadLogToken**](https://msdn.microsoft.com/library/windows/hardware/ff552211) to write log entries in a [text log section](format-of-a-text-log-section.md) that was established by the SetupAPI installation operation that called the installer. SetupAPI text logging also provides system-defined log tokens, which an installation application can use to write log entries that are not part of a text log section.

The following system-defined log tokens are provided by SetupAPI text logging:

<a href="" id="logtoken-unspecified"></a>LOGTOKEN\_UNSPECIFIED  
Represents the part of an unspecified text log that is not part of a [text log section](format-of-a-text-log-section.md). By default, the [SetupAPI logging functions](https://msdn.microsoft.com/library/windows/hardware/ff550878) write a log entry in the application installation text log if this token value is specified.

<a href="" id="logtoken-no-log"></a>LOGTOKEN\_NO\_LOG  
Represents the null log. The SetupAPI logging functions do not write a log entry if this token value is specified.

<a href="" id="logtoken-setupapi-applog"></a>LOGTOKEN\_SETUPAPI\_APPLOG  
Represents the part of the application text log (*SetupAPI.app.log)* that is not part of a text log section. The [SetupAPI logging functions](https://msdn.microsoft.com/library/windows/hardware/ff550878) write log entries in the application installation text log if this token value is specified.

<a href="" id="logtoken-setupapi-devlog"></a>LOGTOKEN\_SETUPAPI\_DEVLOG  
Represents the part of the device installation text log (*SetupAPI.dev.log)* that is not part of a text log section. The SetupAPI logging functions write log entries in the device installation text log if this token value is specified.

 

 





