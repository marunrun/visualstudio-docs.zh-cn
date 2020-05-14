---
title: 初始化功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 661e0a24fa1d222079fd5ee728c5f42a5386c75b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700634"
---
# <a name="sccinitialize-function"></a>SccInitialize 函数
此功能初始化源代码管理插件，并为集成开发环境 （IDE） 提供功能和限制。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccInitialize (
   LPVOID* ppvContext,
   HWND    hWnd,
   LPCSTR  lpCallerName,
   LPSTR   lpSccName,
   LPLONG  lpSccCaps,
   LPSTR   lpAuxPathLabel,
   LPLONG  pnCheckoutCommentLen,
   LPLONG  pnCommentLen
);
```

#### <a name="parameters"></a>参数
 `ppvContext`

[在]源代码管理插件可以在此处放置指向其上下文结构的指针。

 `hWnd`

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 `lpCallerName`

[在]调用源代码管理插件的程序的名称。

 `lpSccName`

[进出]源代码管理插件放置其自己的名称（不要超过`SCC_NAME_LEN`）的缓冲区。

 `lpSccCaps`

[出]返回源代码管理插件的功能标志。

 `lpAuxPathLabel`

[进出]源代码管理插件放置一个字符串，用于描述[SccOpenProject](../extensibility/sccopenproject-function.md)和[SccGetProjPath](../extensibility/sccgetprojpath-function.md)返回的`SCC_AUXLABEL_LEN``lpAuxProjPath`参数（不要超过 ）。

 `pnCheckoutCommentLen`

[出]返回结帐注释的最大允许长度。

 `pnCommentLen`

[出]返回其他注释的最大允许长度。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|源代码管理初始化成功。|
|SCC_E_INITIALIZEFAILED|无法初始化系统。|
|SCC_E_NOTAUTHORIZED|不允许用户执行指定的操作。|
|SCC_E_NONSPECFICERROR|非特异性故障;源控制系统未初始化。|

## <a name="remarks"></a>备注
 IDE 首次加载源代码管理插件时调用此功能。 它使 IDE 能够将某些信息（如调用方名称）传递给插件。 IDE 还会返回某些信息，例如注释的最大允许长度和插件的功能。

 指向`ppvContext`指针`NULL`。 源代码管理插件可以分配一个结构供自己使用，并在 中`ppvContext`存储指向该结构的指针。 IDE 会将此指针传递给所有其他 VSSCI API 函数，允许插件在不使用全局存储的情况下提供上下文信息，并支持插件的多个实例。 调用[SccUn初始化](../extensibility/sccuninitialize-function.md)时，应处理此结构。

 和`lpCallerName``lpSccName`参数使 IDE 和源代码管理插件能够交换名称。 这些名称可能仅用于区分多个实例，或者它们实际上可能显示在菜单或对话框中。

 该`lpAuxPathLabel`参数是一个字符串，用作注释，用于标识存储在解决方案文件中并传递到[SccOpenProject](../extensibility/sccopenproject-function.md)调用中的源代码管理插件的辅助项目路径。 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]使用字符串"源安全项目：";其他源代码管理插件应避免使用此特定字符串。

 该`lpSccCaps`参数为源代码管理插件提供了一个存储指示插件功能的位标志的位置。 （有关功能位标志的完整列表，请参阅[功能标志](../extensibility/capability-flags.md)）。 例如，如果插件计划将结果写入调用方提供的回调函数，则插件将SCC_CAP_TEXTOUT设置功能位。 这将发出 IDE 信号，为版本控制结果创建一个窗口。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [功能标志](../extensibility/capability-flags.md)
