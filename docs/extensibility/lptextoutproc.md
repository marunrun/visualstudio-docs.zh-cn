---
title: LPTEXTOUTPROC | Microsoft Docs
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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a990fc28ffcba4cffc199c1435fddb41bd896521
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309027"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

当用户执行从集成的开发环境 (IDE) 内部的源代码管理操作时，源代码管理插件可能想要传达与操作相关的错误或状态消息。 该插件可以实现此目的中显示其自己的消息框。 但是，对于更多的无缝集成，该插件可以传递字符串到 IDE，然后将它们显示在其本机的显示状态信息的方式。 此机制是`LPTEXTOUTPROC`函数指针。 IDE 实现此函数用于显示错误和状态 （下面更详细地介绍）。

IDE 将传递到源代码管理插件对此函数的函数指针作为`lpTextOutProc`参数，调用时[SccOpenProject](../extensibility/sccopenproject-function.md)。 在源代码管理操作，示例中，中间调用期间[SccGet](../extensibility/sccget-function.md)涉及多个文件，该插件可以调用`LPTEXTOUTPROC`函数，定期传递要显示的字符串。 IDE 可能会显示一个状态栏，在输出窗口中，或在单独的消息中，根据需要这些字符串。 （可选） 可以显示与特定消息可能会在 IDE**取消**按钮。 这使用户能够取消此操作，并为 IDE 提供将此信息传递回该插件的功能。

## <a name="signature"></a>签名
 在 IDE 的输出函数具有以下签名：

```cpp
typedef LONG (*LPTEXTOUTPROC) (
   LPSTR display_string,
   LONG mesg_type
);
```

## <a name="parameters"></a>参数

display_string

要显示的文本字符串。 此字符串不应因一个回车符返回或换行。

mesg_type

消息的类型。 下表列出了支持此参数的值。

|值|描述|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|消息将被视为信息、 警告或错误。|
|`SCC_MSG_STATUS`|显示状态消息，并可以在状态栏中显示。|
|`SCC_MSG_DOCANCEL`|与任何消息字符串一起发送。|
|`SCC_MSG_STARTCANCEL`|开始显示**取消**按钮。|
|`SCC_MSG_STOPCANCEL`|将不再显示**取消**按钮。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|如果后台操作已取消，会要求 IDE:返回 IDE`SCC_MSG_RTN_CANCEL`如果操作已取消; 否则，返回`SCC_MSG_RTN_OK`。 `display_string`参数强制转换为[SccMsgDataIsCancelled](#LinkSccMsgDataIsCancelled)结构，它提供的源代码管理插件。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|从版本控制检索之前关于文件告知 IDE。 `display_string`参数强制转换为[SccMsgDataOnBeforeGetFile](#LinkSccMsgDataOnBeforeGetFile)结构，它提供的源代码管理插件。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|关于文件告知 IDE 后检索从版本控制。 `display_string`参数强制转换为[SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile)结构，它提供的源代码管理插件。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|告知 IDE 的后台操作的当前状态。 `display_string`参数强制转换为[SccMsgDataOnMessage](#LinkSccMsgDataOnMessage)结构，它提供的源代码管理插件。|

## <a name="return-value"></a>返回值

|值|描述|
|-----------|-----------------|
|SCC_MSG_RTN_OK|显示的字符串或操作已成功完成。|
|SCC_MSG_RTN_CANCEL|用户想要取消该操作。|

## <a name="example"></a>示例
 假设 IDE 调用[SccGet](../extensibility/sccget-function.md)使用 20 个文件的名称。 源代码管理插件希望阻止取消中间文件 get 操作。 获取后每个文件，它调用`lpTextOutProc`，将其传递状态信息对每个文件，然后将发送`SCC_MSG_DOCANCEL`消息是否没有报告的状态。 如果在任何时候插件接收返回值的`SCC_MSG_RTN_CANCEL`从 IDE，它会取消获取操作立即，以便检索更多文件。

## <a name="structures"></a>结构

### <a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 此结构发送与`SCC_MSG_BACKGROUND_IS_CANCELLED`消息。 它用于通信的后台操作已取消的 ID。

### <a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 此结构发送与`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`消息。 它用于通信要检索的文件的名称和正在执行的操作检索的后台操作的 ID。

### <a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 此结构发送与`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`消息。 它用于检索指定的文件，以及未检索的后台操作的 ID 的结果进行通信。 请参阅的返回值[SccGet](../extensibility/sccget-function.md)有关什么可以给出结果。

### <a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 此结构发送与`SCC_MSG_BACKGROUND_ON_MESSAGE`消息。 它用于通信的后台操作的当前状态。 状态表示为一个字符串，要显示的 IDE，并`bIsError`指示消息的严重性 (`TRUE`为一条错误消息;`FALSE`警告或信息性消息)。 此外还提供发送状态的后台操作的 ID。

## <a name="code-example"></a>代码示例
 下面是调用的简单示例`LPTEXTOUTPROC`发送`SCC_MSG_BACKGROUND_ON_MESSAGE`消息，显示如何调用转换结构。

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
- [通过 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)