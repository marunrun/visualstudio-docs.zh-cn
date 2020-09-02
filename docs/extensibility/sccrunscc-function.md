---
title: SccRunScc 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 n

中数组中指定的文件数 `lpFileNames` 。

 lpFileNames

中选定文件名的数组。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功调用源代码管理工具。|
|SCC_I_OPERATIONCANCELED|操作已取消。|
|SCC_E_INITIALIZEFAILED|未能初始化源代码管理系统。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。|
|SCC_E_CONNECTIONFAILURE|未能连接到源代码管理系统。|
|SCC_E_FILENOTCONTROLLED|所选文件不受源代码管理。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数允许调用方通过外部管理工具访问源代码管理系统的全部功能。 如果源代码管理系统没有用户界面，则源代码管理插件可以实现接口，以执行所需的管理功能。

 使用当前所选文件的计数和文件名数组调用此函数。 如果管理工具支持它，则可以使用文件列表在管理界面中预选文件;否则，可以忽略此列表。

 当用户从 "**文件**源控制" 菜单中**选择 \<Source Control Server> 启动**时，通常会调用此函数  ->  **Source Control** 。 可以通过设置注册表项来始终禁用或甚至隐藏此 " **启动** " 菜单选项。 有关详细信息，请参阅 [如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md) 。 仅当 [SccInitialize](../extensibility/sccinitialize-function.md) 返回功能位时才会调用此函数 `SCC_CAP_RUNSCC` 。有关此功能位和其他功能位) 的详细信息，请参阅 [功能标志](../extensibility/capability-flags.md) (。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [如何：安装源代码管理插件](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [功能标志](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
