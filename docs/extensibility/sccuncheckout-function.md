---
title: SccUncheck 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4317133b2f215e0f9af447e5c042785561231f63
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700251"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 函数
此函数撤消以前的签出操作，从而在签出之前将所选文件或文件的内容还原到状态。 结帐后对文件所做的所有更改都丢失。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccUncheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>参数
 pvContext

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 n文件

[在]`lpFileNames`数组中指定的文件数。

 lpFile名称

[在]要撤消签出的文件完全限定的本地路径名称的数组。

 fOptions

[在]命令标志（未使用）。

 pvOptions

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|撤消签出成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不受源代码控制。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特异性故障。 撤消签出未成功。|
|SCC_E_NOTCHECKEDOUT|用户未签出该文件。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_PROJNOTOPEN|尚未从源代码管理打开该项目。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="remarks"></a>备注
 此操作后，将清除`SCC_STATUS_CHECKEDOUT``SCC_STATUS_MODIFIED`执行撤消签出的文件 的 和 标志。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
