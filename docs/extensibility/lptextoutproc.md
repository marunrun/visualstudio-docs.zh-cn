---
title: LPTEXTOUTPROC |Microsoft Docs
description: 了解 LPTEXTOUTPROC 函数指针。 Visual Studio IDE 实现了用于显示错误和状态的函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- LPTEXTOUTPROC
helpviewer_keywords:
- SccMsgDataOnMessage structure
- SccMsgDataOnBeforeGetFile structure
- SccMsgDataIsCancelled structure
- LPTEXTOUTPROC callback function
- SccMsgDataOnAfterGetFile structure
ms.assetid: 2025c969-e3c7-4cf4-a5c5-099d342895ea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a04f47a6500c0cd2174d0567029a4f5c86d9f62d
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97615722"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

当用户从集成开发环境内部 (IDE) 执行源代码管理操作时，源代码管理插件可能需要传达与操作相关的错误或状态消息。 此插件可以显示其自己的消息框以实现此目的。 但是，为了实现更无缝的集成，该插件可将字符串传递到 IDE，然后以其本机方式显示状态信息。 此的机制是 `LPTEXTOUTPROC` 函数指针。 IDE 将更详细地实现此函数 (，) 以显示错误和状态。

`lpTextOutProc`调用[SccOpenProject](../extensibility/sccopenproject-function.md)时，IDE 会将此函数的函数指针作为参数传递给源代码管理插件。 在 SCC 操作期间（例如，在调用涉及多个文件的 [SccGet](../extensibility/sccget-function.md) 的过程中），插件可以调用 `LPTEXTOUTPROC` 函数，并定期传递要显示的字符串。 IDE 可能会将这些字符串显示在状态栏、输出窗口或单独的消息框中（视情况而不同）。 IDE 还可以使用 " **取消** " 按钮显示某些消息。 这样，用户就可以取消操作，并为 IDE 提供将此信息传递回插件的功能。

## <a name="signature"></a>签名
 IDE 的 output 函数具有以下签名：

```cpp
typedef LONG (*LPTEXTOUTPROC) (
   LPSTR display_string,
   LONG mesg_type
);
```

## <a name="parameters"></a>参数

display_string

要显示的文本字符串。 不应使用回车符或换行符终止此字符串。

mesg_type

消息的类型。 下表列出了此参数支持的值。

|值|说明|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|消息被视为信息、警告或错误。|
|`SCC_MSG_STATUS`|此消息显示状态，并且可以显示在状态栏中。|
|`SCC_MSG_DOCANCEL`|发送时不包含消息字符串。|
|`SCC_MSG_STARTCANCEL`|开始显示 " **取消** " 按钮。|
|`SCC_MSG_STOPCANCEL`|停止显示 " **取消** " 按钮。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|如果后台操作被取消，则会询问 IDE： IDE 将 `SCC_MSG_RTN_CANCEL` 在取消操作时返回; 否则返回 `SCC_MSG_RTN_OK` 。 `display_string`参数将强制转换为[SccMsgDataIsCancelled](#LinkSccMsgDataIsCancelled)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|从版本控制中检索文件之前通知 IDE。 `display_string`参数将强制转换为[SccMsgDataOnBeforeGetFile](#LinkSccMsgDataOnBeforeGetFile)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|从版本控制中检索文件后，告诉 IDE 文件。 `display_string`参数将强制转换为[SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|告诉 IDE 后台操作的当前状态。 `display_string`参数将强制转换为[SccMsgDataOnMessage](#LinkSccMsgDataOnMessage)结构，该结构由源代码管理插件提供。|

## <a name="return-value"></a>返回值

|值|说明|
|-----------|-----------------|
|SCC_MSG_RTN_OK|字符串已显示或操作已成功完成。|
|SCC_MSG_RTN_CANCEL|用户要取消该操作。|

## <a name="example"></a>示例
 假设 IDE 调用了包含二十个文件名的 [SccGet](../extensibility/sccget-function.md) 。 源代码管理插件希望阻止在文件获取过程中取消该操作。 获取每个文件后，它会调用并向 `lpTextOutProc` 其传递每个文件的状态信息，并在 `SCC_MSG_DOCANCEL` 消息没有要报告的状态时发送消息。 如果插件从 IDE 中收到返回值 `SCC_MSG_RTN_CANCEL` ，则会立即取消 get 操作，以便不会再检索文件。

## <a name="structures"></a>結構

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 此结构随消息一起发送 `SCC_MSG_BACKGROUND_IS_CANCELLED` 。 它用于传达已取消的后台操作的 ID。

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 此结构随消息一起发送 `SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE` 。 它用于传递要检索的文件的名称，以及正在执行检索操作的后台操作的 ID。

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 此结构随消息一起发送 `SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE` 。 它用于传递检索指定文件的结果，以及执行检索操作的后台操作的 ID。 请参阅 [SccGet](../extensibility/sccget-function.md) 的返回值，以了解可获得的结果。

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 此结构随消息一起发送 `SCC_MSG_BACKGROUND_ON_MESSAGE` 。 它用于传达后台操作的当前状态。 状态表示为一个字符串，该字符串将由 IDE 显示，并 `bIsError` 指明错误消息 (消息的严重性 `TRUE` ; `FALSE` 对于警告或) ，为信息性消息。 同时提供发送状态的后台操作的 ID。

## <a name="code-example"></a>代码示例
 下面是调用发送消息的简单示例 `LPTEXTOUTPROC` `SCC_MSG_BACKGROUND_ON_MESSAGE` ，演示如何转换调用的结构。

```cpp
LONG SendStatusMessage(
    LPTEXTOUTPROC pTextOutProc,
    DWORD         dwBackgroundID,
    LPCTSTR       pStatusMsg,
    BOOL          bIsError)
{
    SccMsgDataOnMessage msgData = { 0 };
    LONG                result  = 0;

    msgData.dwBackgroundOperationID = dwBackgroundID;
    msgData.szMessage               = pStatusMsg;
    msgData.bIsError                = bIsError;

    result = pTextOutProc(reinterpret_cast<LPCTSTR>(&msgData), SCC_MSG_BACKGROUND_ON_MESSAGE);
    return result;
}
```

## <a name="see-also"></a>另请参阅
- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
