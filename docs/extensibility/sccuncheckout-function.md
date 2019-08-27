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
ms.openlocfilehash: 4d50b321f96b6759d95a6d923222e5e0a92b2ee3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338463"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 函数
此函数撤消以前的签出操作，从而将所选的文件或文件的内容还原到之前签出状态。 签出后对文件所做的所有更改都都将丢失。

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

[in]源控制插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 nFiles

[in]中指定的文件数`lpFileNames`数组。

 lpFileNames

[in]要撤消签出文件的完全限定的本地路径名称的数组。

 fOptions

[in]（未使用） 的命令标志。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|撤消签出成功。|
|SCC_E_FILENOTCONTROLLED|所选的文件不是源代码管理下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。 撤消签出失败。|
|SCC_E_NOTCHECKEDOUT|用户不具有签出文件。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_PROJNOTOPEN|未从源代码管理打开项目。|
|SCC_I_OPERATIONCANCELED|在完成之前已取消操作。|

## <a name="remarks"></a>备注
 执行此操作后`SCC_STATUS_CHECKEDOUT`和`SCC_STATUS_MODIFIED`标志会同时为清除对其执行撤消签出的文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)