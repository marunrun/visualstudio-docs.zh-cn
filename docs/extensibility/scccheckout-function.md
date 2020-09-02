---
title: SccCheckout 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6ed809e33a80bf2903c88550e97b28b1e0178bcd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701105"
---
# <a name="scccheckout-function"></a>SccCheckout 函数
提供完全限定的文件名的列表后，此函数会将其签出到本地驱动器。 注释适用于所有正在签出的文件。Comment 参数可以是一个 `null` 字符串。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 n

中选择要签出的文件数。

 lpFileNames

中要签出的文件的完全限定的本地路径名称数组。

 lpComment

中要应用到每个已签出的所选文件的注释。

 用于

中命令标志 (参阅) [使用的特定命令所使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功签出。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码管理下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|非特定故障。 文件未签出。|
|SCC_E_ALREADYCHECKEDOUT|用户已签出文件。|
|SCC_E_FILEISLOCKED|文件被锁定，禁止创建新版本。|
|SCC_E_FILEOUTEXCLUSIVE|其他用户已在此文件上执行了独占签出。|
|SCC_I_OPERATIONCANCELED|操作在完成前被取消。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md)
