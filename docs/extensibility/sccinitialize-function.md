---
title: SccInitialize 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700634"
---
# <a name="sccinitialize-function"></a>SccInitialize 函数
此函数初始化源代码管理插件，并向集成开发环境 (IDE) 提供功能和限制。

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

中源代码管理插件可在此处放置指向其上下文结构的指针。

 `hWnd`

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 `lpCallerName`

中调用源代码管理插件的程序的名称。

 `lpSccName`

[in，out]源代码管理插件将其自己的名称放 (不超过) 的缓冲区 `SCC_NAME_LEN` 。

 `lpSccCaps`

弄返回源代码管理插件的功能标志。

 `lpAuxPathLabel`

[in，out]一个缓冲区，其中，源代码管理插件将描述 `lpAuxProjPath` [SccOpenProject](../extensibility/sccopenproject-function.md) 返回参数的字符串，而 [SccGetProjPath](../extensibility/sccgetprojpath-function.md) (不超过 `SCC_AUXLABEL_LEN`) 。

 `pnCheckoutCommentLen`

弄返回签出注释允许的最大长度。

 `pnCommentLen`

弄返回其他注释允许的最大长度。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|源代码管理初始化成功。|
|SCC_E_INITIALIZEFAILED|系统无法初始化。|
|SCC_E_NOTAUTHORIZED|不允许用户执行指定的操作。|
|SCC_E_NONSPECFICERROR|模糊失败;源代码管理系统未初始化。|

## <a name="remarks"></a>备注
 IDE 首次加载源代码管理插件时将调用此函数。 它使 IDE 能够将某些信息（例如调用方名称）传递到插件。 IDE 还会返回某些信息，如注释的最大允许长度和插件的功能。

 指向 `ppvContext` `NULL` 指针的指针。 源代码管理插件可以为自己的使用分配结构，并在中存储指向该结构的指针 `ppvContext` 。 IDE 将向每个其他 VSSCI API 函数传递此指针，使插件可以在不使用全局存储的情况下提供上下文信息，并支持插件的多个实例。 调用 [SccUninitialize](../extensibility/sccuninitialize-function.md) 时应释放此结构。

 `lpCallerName`和 `lpSccName` 参数使 IDE 和源代码管理插件能够交换名称。 这些名称可以简单地用于区分多个实例，也可以实际出现在菜单或对话框中。

 `lpAuxPathLabel`参数是一个字符串，用作注释以标识存储在解决方案文件中的辅助项目路径，并在对[SccOpenProject](../extensibility/sccopenproject-function.md)的调用中传递到源代码管理插件。 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] 使用字符串 "SourceSafe 项目：";其他源代码管理插件应避免使用此特定字符串。

 `lpSccCaps`参数为源代码管理插件提供了一个用于存储 bitflags 的位置，用于指示插件的功能。  (获取功能 bitflags 的完整列表，请参阅 [功能标志](../extensibility/capability-flags.md)) 。 例如，如果插件计划将结果写入调用方提供的回调函数，该插件会将功能位设置 SCC_CAP_TEXTOUT。 这会通知 IDE 创建版本控制结果的窗口。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [功能标志](../extensibility/capability-flags.md)
