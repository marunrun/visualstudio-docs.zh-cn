---
title: sccrename 函数 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 88a917e43729b3049e488264c260f8455ab08fe4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700429"
---
# <a name="sccrename-function"></a>SccRename 函数
此函数重命名源代码管理系统中的文件。

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

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpFile名称

[在]要重命名的文件的完全限定文件名。

 lp 新名称

[在]完全限定的新名称。 如果目录路径不同，则文件已从一个子目录移动到另一个子目录。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|重命名操作已成功完成。|
|SCC_E_PROJNOTOPEN|项目在源代码管理下不开放。|
|SCC_E_FILENOTCONTROLLED|该文件不受源代码管理。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。|
|SCC_E_NOTAUTHORIZED|用户无权完成此操作。|
|SCC_E_COULDNOTCREATEPROJECT|无法作为重命名过程的一部分创建项目。|
|SCC_E_OPNOTPERFORMED|未执行操作。|
|SCC_E_NONSPECIFICERROR|发生未指定或常规错误。|

## <a name="remarks"></a>备注
 此功能可用于重命名文件或将其从一个位置移动到源代码管理系统中的另一个位置。 源代码管理插件不应尝试访问磁盘上的文件。 IDE 负责重命名本地文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
