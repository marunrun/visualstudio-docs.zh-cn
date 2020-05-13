---
title: Sccadd文件从SCC功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d22527644edbf1697112f5cf8b73b8a3f72b774
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701290"
---
# <a name="sccaddfilesfromscc-function"></a>SCC 函数中包含文件
此函数将文件列表从源代码管理添加到当前打开的项目。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccAddFilesFromSCC(
   LPVOID  pContext,
   HWND    hWnd,
   LPSTR   lpUser,
   LPSTR   lpAuxProjPath,
   LONG    cFiles,
   LPCSTR* lpFilePaths,
   LPCSTR  lpDestination,
   LPCSTR  lpComment,
   LPBOOL  pbResults
);
```

### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文指针。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpUser

[进出]用户名（最多SCC_USER_SIZE，包括空终止符）。

 lpAuxProjPath

[进出]标识项目的辅助字符串（最多`SCC_PRJPATH_`大小，包括空终止符）。

 cFiles

[在]提供`lpFilePaths`的文件数。

 lpFilePath

[进出]要添加到当前项目的文件名数组。

 lp目标

[在]要写入文件的目标路径。

 lpComment

[在]要应用于要添加到的每个文件的注释。

 pb 结果

[进出]设置为指示每个文件成功（非零或 TRUE）或失败（零或 FALSE）的标志数组（数组的大小必须至少`cFiles`为长）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_E_PROJNOTOPEN|项目未打开。|
|SCC_E_OPNOTPERFORMED|连接与指定的项目不同`lpAuxProjPath.`|
|SCC_E_NOTAUTHORIZED|用户无权更新数据库。|
|SCC_E_NONSPECIFICERROR|未知错误。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
