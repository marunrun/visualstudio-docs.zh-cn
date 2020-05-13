---
title: SccRunScc 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d012908e59be8b82e34ff68cdab1945c5bd2de8b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700397"
---
# <a name="sccrunscc-function"></a>SccRunScc 函数
此函数调用源代码管理工具。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccRunScc(
   LPVOID  pvContext,
   HWND    hWnd,
   LONG    nFiles,
   LPCSTR* lpFileNames
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

[在]所选文件名的数组。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功调用源代码管理工具。|
|SCC_I_OPERATIONCANCELED|操作已取消。|
|SCC_E_INITIALIZEFAILED|无法初始化源代码管理系统。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。|
|SCC_E_CONNECTIONFAILURE|无法连接到源代码管理系统。|
|SCC_E_FILENOTCONTROLLED|所选文件不受源代码管理。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 此功能允许调用方通过外部管理工具访问源代码管理系统的全部功能。 如果源代码管理系统没有用户界面，源代码管理插件可以实现一个接口来执行必要的管理功能。

 此函数使用当前选定文件的 count 和文件名数组进行调用。 如果管理工具支持它，则文件列表可用于在管理界面中预先选择文件;如果管理工具支持它，则文件列表可用于预先选择管理界面中的文件。否则，可以忽略该列表。

 当用户从 **"文件** -> **源控制"** 菜单中选择**启动\<源控制服务器>** 时，通常会调用此功能。 通过设置注册表项，始终可以禁用甚至隐藏此**启动**菜单选项。 有关详细信息[，请参阅：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)。 仅当[Scc初始化](../extensibility/sccinitialize-function.md)返回`SCC_CAP_RUNSCC`功能位时，才会调用此功能（有关此功能位和其他功能位的详细信息，请参阅[功能标志](../extensibility/capability-flags.md)）。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [功能标志](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
