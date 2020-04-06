---
title: SccEnum更改文件功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b1826a87b20d6bc92254fc4a86b8e0b756400ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700908"
---
# <a name="sccenumchangedfiles-function"></a>SccEnum 更改文件功能
给定本地文件的列表，此函数确定哪些文件不同于源代码管理数据库中的相应版本。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccEnumChangedFiles(
   LPVOID  pContext,
   HWND    hWnd,
   LONG    cFiles,
   LPCSTR* lpFileNames,
   LONG*   plIsFileDifferent
);
```

### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文指针。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 cFiles

[在]`lpFileNames`数组中指定的文件名数。 还指定数组的大小`plIsFileDifferent`。

 lpFile名称

[在]要检查的本地文件名数组。

 plIsFile不同

[进出]指示每个文件差异状态的值数组（数组必须至少有`cFiles`条目）。 非零表示文件不同。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|操作已成功完成。|
|SCC_UNSPECIFIEDERROR|常规错误。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
