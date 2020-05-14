---
title: SccCheckout 功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701105"
---
# <a name="scccheckout-function"></a>SccCheckout 功能
给定完全限定的文件名列表，此函数会将它们签出到本地驱动器。 注释应用于签出的所有文件。注释参数可以是字符串`null`。

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

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 n文件

[在]选择要签出的文件数。

 lpFile名称

[在]要签出的文件完全限定的本地路径名称的数组。

 lpComment

[在]要应用于要签出的每个选定文件的注释。

 fOptions

[在]命令标志（请参阅[特定命令使用的比特标志](../extensibility/bitflags-used-by-specific-commands.md)）。

 pvOptions

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|退房成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不受源代码控制。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_NONSPECIFICERROR|非特异性故障。 文件未签出。|
|SCC_E_ALREADYCHECKEDOUT|用户已签出该文件。|
|SCC_E_FILEISLOCKED|该文件已锁定，禁止创建新版本。|
|SCC_E_FILEOUTEXCLUSIVE|其他用户已对此文件执行独占签出。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的比特标志](../extensibility/bitflags-used-by-specific-commands.md)
