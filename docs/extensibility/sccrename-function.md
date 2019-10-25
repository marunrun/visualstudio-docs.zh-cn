---
title: SccRename 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30b2928653507b670160c72ca3ce09a0227a4170
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720770"
---
# <a name="sccrename-function"></a>SccRename 函数
此函数将重命名源代码管理系统中的文件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccRename(
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName,
   LPCSTR lpNewName
);
```

#### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpFileName

中要重命名的文件的完全限定文件名。

 lpNewName

中完全限定的新名称。 如果目录路径不同，则文件已从一个子目录移到另一个子目录。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|重命名操作已成功完成。|
|SCC_E_PROJNOTOPEN|未在源代码管理下打开该项目。|
|SCC_E_FILENOTCONTROLLED|此文件不受源代码管理。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。|
|SCC_E_NOTAUTHORIZED|用户无权完成此操作。|
|SCC_E_COULDNOTCREATEPROJECT|无法将该项目作为重命名过程的一部分来创建。|
|SCC_E_OPNOTPERFORMED|未执行此操作。|
|SCC_E_NONSPECIFICERROR|出现未指定的错误或常规错误。|

## <a name="remarks"></a>备注
 此函数可用于重命名文件，或将其从源控制系统中的一个位置移动到另一个位置。 源代码管理插件不应尝试访问磁盘上的文件。 重命名本地文件是 IDE 的责任。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)