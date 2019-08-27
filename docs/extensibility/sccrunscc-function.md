---
title: SccRunScc 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec6f430b4fee28e0bd1a9d5b1c64f9e8d95b2a97
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338698"
---
# <a name="sccrunscc-function"></a>SccRunScc 函数
此函数调用的源代码管理管理工具。

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

[in]源控制插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 nFiles

[in]中指定的文件数`lpFileNames`数组。

 lpFileNames

[in]所选的文件名称的数组。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功调用源控件管理工具。|
|SCC_I_OPERATIONCANCELED|已取消该操作。|
|SCC_E_INITIALIZEFAILED|无法初始化源代码管理系统。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。|
|SCC_E_CONNECTIONFAILURE|无法连接到源代码管理系统。|
|SCC_E_FILENOTCONTROLLED|所选的文件不受源代码管理中。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数允许调用方通过外部管理工具访问的完整范围的源控制系统的功能。 如果源代码管理系统有没有用户界面，源代码管理插件可以实现接口，以执行必要的管理功能。

 使用计数和当前所选文件的文件名称的数组调用此函数。 如果管理工具支持，可以使用的文件列表预先选择管理界面; 中的文件否则，可以忽略列表。

 当用户选择时，通常调用此函数**启动\<源代码管理服务器 >** 从**文件** -> **源代码管理**菜单。 这**启动**菜单选项可以始终处于禁用状态，或甚至隐藏通过设置注册表项。 请参阅[如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)有关详细信息。 仅当调用此函数[SccInitialize](../extensibility/sccinitialize-function.md)返回`SCC_CAP_RUNSCC`功能位 (请参阅[功能标志](../extensibility/capability-flags.md)有关此权益以及其他功能位的详细信息)。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [功能标志](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)