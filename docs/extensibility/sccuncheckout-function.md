---
title: SccUncheckout 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e35d7287d8fc12100da9ba3b8383d8e92cee73d4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720534"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 函数
此函数将撤消以前的签出操作，从而将所选文件的内容还原到结帐之前的状态。 自签出后对文件进行的所有更改都将丢失。

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

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 n

中@No__t_0 数组中指定的文件数。

 lpFileNames

中要撤消签出的文件的完全限定的本地路径名称数组。

 用于

中命令标志（未使用）。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|撤消签出成功。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码管理下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。 撤消签出失败。|
|SCC_E_NOTCHECKEDOUT|用户未签出文件。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_PROJNOTOPEN|尚未从源代码管理中打开该项目。|
|SCC_I_OPERATIONCANCELED|操作在完成前被取消。|

## <a name="remarks"></a>备注
 完成此操作后，将为执行撤消签出的文件清除 `SCC_STATUS_CHECKEDOUT` 和 `SCC_STATUS_MODIFIED` 标志。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)