---
title: LPTEXTOUTPROC |微软文档
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
ms.openlocfilehash: 38c3e8263b9a30058c2de019e5e92160b716aa71
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702793"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

当用户从集成开发环境 （IDE） 内部执行源代码管理操作时，源代码管理插件可能需要传达与操作相关的错误或状态消息。 为此，插件可以显示自己的消息框。 但是，为了进行更无缝的集成，插件可以将字符串传递给 IDE，IDE 然后以本机方式显示状态信息。 这是`LPTEXTOUTPROC`函数指针。 IDE 实现此函数（下面将详细介绍），用于显示错误和状态。

调用`lpTextOutProc`[SccOpenProject](../extensibility/sccopenproject-function.md)时，IDE 将函数指针传递给此函数（作为参数）传递给源代码管理插件。 例如，在 SCC 操作期间，在调用涉及许多文件的[SccGet](../extensibility/sccget-function.md)时，插件可以调用`LPTEXTOUTPROC`该函数，定期传递字符串以显示。 IDE 可以根据需要在状态栏、输出窗口中或单独的消息框中显示这些字符串。 或者，IDE 可能可以使用 **"取消"** 按钮显示某些消息。 这使用户能够取消该操作，并使 IDE 能够将此信息传回插件。

## <a name="signature"></a>签名
 IDE 的输出函数具有以下签名：

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

消息的类型。 下表列出了此参数的支持值。

|值|说明|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|该消息被视为信息、警告或错误。|
|`SCC_MSG_STATUS`|该消息显示状态，可以显示在状态栏中。|
|`SCC_MSG_DOCANCEL`|未发送消息字符串。|
|`SCC_MSG_STARTCANCEL`|开始显示 **"取消"** 按钮。|
|`SCC_MSG_STOPCANCEL`|停止显示 **"取消"** 按钮。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|询问 IDE 是否要取消后台操作：如果操作被取消`SCC_MSG_RTN_CANCEL`，IDE 将返回;否则，返回`SCC_MSG_RTN_OK`。 该`display_string`参数被强制转换为[SccMsgDataIsCanceled](#LinkSccMsgDataIsCancelled)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|在从版本控件检索文件之前，先向 IDE 介绍该文件。 该`display_string`参数被强制转换为[SccMsgDataOnOnGetFile](#LinkSccMsgDataOnBeforeGetFile)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|从版本控件检索文件后，向 IDE 告知该文件。 该`display_string`参数被强制转换为[SccMsgDataOnOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|告诉 IDE 后台操作的当前状态。 该`display_string`参数被强制转换为[SccMsgDataOnMessage](#LinkSccMsgDataOnMessage)结构，该结构由源代码管理插件提供。|

## <a name="return-value"></a>返回值

|值|说明|
|-----------|-----------------|
|SCC_MSG_RTN_OK|显示字符串或操作已成功完成。|
|SCC_MSG_RTN_CANCEL|用户希望取消该操作。|

## <a name="example"></a>示例
 假设 IDE 调用具有 20 个文件名[的 SccGet。](../extensibility/sccget-function.md) 源代码管理插件希望防止在文件获取中间取消操作。 获取每个文件后，它会调用`lpTextOutProc`，传递每个文件的状态信息，如果该文件没有要报告的状态`SCC_MSG_DOCANCEL`，则发送消息。 如果插件在任何时候收到来自 IDE 的`SCC_MSG_RTN_CANCEL`返回值，它会立即取消 get 操作，以便不再检索文件。

## <a name="structures"></a>结构

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a>SccMsgDatais 已取消

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 此结构随消息一`SCC_MSG_BACKGROUND_IS_CANCELLED`起发送。 它用于传达已取消的背景操作的 ID。

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a>SccMsgDataon 之前获取文件

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 此结构随消息一`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`起发送。 它用于传达要检索的文件的名称和执行检索的后台操作的 ID。

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a>SccMsgdataon 后获取文件

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 此结构随消息一`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`起发送。 它用于传达检索指定文件的结果以及进行检索的后台操作的 ID。 有关可以因此提供的内容，请参阅[SccGet](../extensibility/sccget-function.md)的返回值。

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a>SccMsgDataon消息

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 此结构随消息一`SCC_MSG_BACKGROUND_ON_MESSAGE`起发送。 它用于传达后台操作的当前状态。 状态表示为 IDE 显示的字符串，并`bIsError`指示消息的严重性（`TRUE`对于错误消息;`FALSE`用于警告或信息性消息）。 还提供了发送状态的后台操作的 ID。

## <a name="code-example"></a>代码示例
 下面是调用`LPTEXTOUTPROC`发送消息的简短`SCC_MSG_BACKGROUND_ON_MESSAGE`示例，演示如何为调用强制转换结构。

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

## <a name="see-also"></a>请参阅
- [IDE 实现的回调功能](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
