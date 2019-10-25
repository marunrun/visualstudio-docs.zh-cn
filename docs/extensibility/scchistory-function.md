---
title: SccHistory 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0ce0b38b8e602688875549edbac671e664809482
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721247"
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

中源代码管理插件上下文结构。

 `hWnd`

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 `nFiles`

中@No__t_0 数组中指定的文件数。

 `lpFileName`

中文件的完全限定名的数组。

 `fOptions`

中命令标志（当前未使用）。

 `pvOptions`

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|已成功获得版本历史记录。|
|SCC_I_RELOADFILE|源代码管理系统在提取历史记录时实际上修改了磁盘上的文件（例如，通过获取其旧版本），因此 IDE 应重新加载此文件。|
|SCC_E_FILENOTCONTROLLED|此文件不受源代码管理。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_PROJNOTOPEN|项目尚未打开。|
|SCC_E_NONSPECIFICERROR|非特定故障。 未能获取文件历史记录。|

## <a name="remarks"></a>备注
 源代码管理插件可以显示自己的对话框以显示每个文件的历史记录，并使用 `hWnd` 作为父窗口。 此外，还可以使用提供给[SccOpenProject](../extensibility/sccopenproject-function.md)的可选文本输出回调函数（如果支持）。

 请注意，在某些情况下，在执行此调用期间，检查的文件可能会发生更改。 例如，[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] history 命令使用户有机会获取旧版本的文件。 在这种情况下，源代码管理插件会返回 `SCC_I_RELOAD` 以警告 IDE 需要重新加载文件。

> [!NOTE]
> 如果源代码管理插件不支持文件数组的此函数，则只能显示第一个文件的文件历史记录。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)