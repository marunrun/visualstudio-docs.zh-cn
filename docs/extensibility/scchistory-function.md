---
title: 历史函数 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 734afefd97e61867076d487acbcf67f10f54e672
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700663"
---
# <a name="scchistory-function"></a>SccHistory 函数
此函数显示指定文件的历史记录。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccHistory(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>参数
 `pvContext`

[在]源代码管理插件上下文结构。

 `hWnd`

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 `nFiles`

[在]`lpFileName`数组中指定的文件数。

 `lpFileName`

[在]文件完全限定名称的数组。

 `fOptions`

[在]命令标志（当前未使用）。

 `pvOptions`

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功获取版本历史记录。|
|SCC_I_RELOADFILE|源代码管理系统实际上在获取历史记录时修改了磁盘上的文件（例如，通过获取其旧版本），因此 IDE 应重新加载此文件。|
|SCC_E_FILENOTCONTROLLED|该文件不受源代码管理。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_PROJNOTOPEN|项目尚未打开。|
|SCC_E_NONSPECIFICERROR|非特异性故障。 无法获取文件历史记录。|

## <a name="remarks"></a>备注
 源代码管理插件可以显示其自己的对话框，以显示每个文件的历史记录，用作`hWnd`父窗口。 或者，如果支持，可以使用提供给[SccOpenProject](../extensibility/sccopenproject-function.md)的可选文本输出回调功能。

 请注意，在某些情况下，正在检查的文件可能会在执行此调用期间更改。 例如，[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]历史记录命令为用户提供了获取文件旧版本的机会。 在这种情况下，源代码管理插件将返回`SCC_I_RELOAD`以警告 IDE 需要重新加载文件。

> [!NOTE]
> 如果源代码管理插件不支持该文件数组的此功能，则只能显示第一个文件的文件历史记录。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
