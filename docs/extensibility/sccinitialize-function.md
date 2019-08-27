---
title: SccInitialize 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a855ecbc65211234b29808fc9e4cf256cd6b25f7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353589"
---
# <a name="sccinitialize-function"></a>SccInitialize 函数
此函数初始化源代码管理插件，并提供了功能和对集成的开发环境 (IDE) 的限制。

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

[in]源代码管理插件可以放置其上下文结构的指针。

 `hWnd`

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 `lpCallerName`

[in]调用源代码管理插件的程序的名称。

 `lpSccName`

[in、 out]源代码管理插件其中放入其自己的名称的缓冲区 (不能超过`SCC_NAME_LEN`)。

 `lpSccCaps`

[out]返回源代码管理插件的功能标志。

 `lpAuxPathLabel`

[in、 out]源代码管理插件将一个字符串，描述其中的缓冲区`lpAuxProjPath`返回参数[SccOpenProject](../extensibility/sccopenproject-function.md)并且[SccGetProjPath](../extensibility/sccgetprojpath-function.md) (不能超过`SCC_AUXLABEL_LEN`)。

 `pnCheckoutCommentLen`

[out]返回签出注释的最大允许长度。

 `pnCommentLen`

[out]返回其他注释的最大允许长度。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|源控件初始化成功。|
|SCC_E_INITIALIZEFAILED|无法初始化系统。|
|SCC_E_NOTAUTHORIZED|不允许用户以执行指定的操作。|
|SCC_E_NONSPECFICERROR|非特定故障;未初始化源代码管理系统。|

## <a name="remarks"></a>备注
 它首次加载源代码管理插件时，IDE 将调用此函数。 这样，IDE 将某些信息，例如调用方名称、 的插件。 IDE 还获取返回某些信息如注释和插件的功能的最大允许长度。

 `ppvContext`指向`NULL`指针。 源代码管理插件可以分配供自己使用的结构和存储指向该结构中的`ppvContext`。 IDE 会将此指针传递到每个其他 VSSCI API 函数时，允许插件而不必求助于全局存储中有可用的上下文信息和支持的插件的多个实例。 此结构应为时已取消分配[SccUninitialize](../extensibility/sccuninitialize-function.md)调用。

 `lpCallerName`和`lpSccName`参数，在 IDE 和源代码管理插件来交换名称。 这些名称只可用于区分多个实例，或者它们可能会实际出现在菜单或对话框。

 `lpAuxPathLabel`参数是为一个注释用于标识存储在解决方案文件，并传递到源代码管理插件的调用中的辅助项目路径的字符串[SccOpenProject](../extensibility/sccopenproject-function.md)。 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] 使用字符串"SourceSafe 项目:";其他源代码管理插件应避免在使用此特定字符串。

 `lpSccCaps`参数提供了源代码管理插件一个位置来存储位标志，指示即插即用的项的功能。 (有关功能位标志的完整列表，请参阅[功能标志](../extensibility/capability-flags.md))。 例如，如果将结果写到调用方提供的回调函数，该插件将设置功能的插件计划位 SCC_CAP_TEXTOUT。 这会发出信号 IDE 来创建一个用于版本控制结果的窗口。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [功能标志](../extensibility/capability-flags.md)