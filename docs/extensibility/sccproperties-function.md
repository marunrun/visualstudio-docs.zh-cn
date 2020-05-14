---
title: Scc属性功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf2dd87efbb50346093144db6e069eea30138e37
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700510"
---
# <a name="sccproperties-function"></a>SccProperties 函数
此函数显示文件或项目的源代码管理属性。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccProperties (
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName
);
```

#### <a name="parameters"></a>参数
 pvContext

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpFile名称

[在]文件或项目的完全限定路径名称。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功显示属性。|
|SCC_I_RELOADFILE|版本控制系统已修改文件属性，因此 IDE 应重新加载此文件。|
|SCC_E_PROJNOTOPEN|未在源代码管理中打开指定的项目。|
|SCC_E_NOTAUTHORIZED|用户无权查看此文件或项目的属性。|
|SCC_E_FILENOTCONTROLLED|指定的文件或项目不受源代码管理。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|发生未知或常规错误。|

## <a name="remarks"></a>备注
 源代码管理插件在其自己的对话框中显示属性。

 属性由源代码管理插件定义，可能因插件而异。 如果插件允许用户更改文件的源代码管理属性，则应返回`SCC_I_RELOAD`以向 IDE 发出信号，指出需要重新加载此文件或项目。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
