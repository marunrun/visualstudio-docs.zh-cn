---
title: SccAddFilesFromSCC 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701290"
---
# <a name="sccaddfilesfromscc-function"></a>SccAddFilesFromSCC 函数
此函数将源代码管理中的文件列表添加到当前打开的项目中。

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

中源代码管理插件上下文指针。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpUser

[in，out]用户名最多 (SCC_USER_SIZE，包括 null 终止符) 。

 lpAuxProjPath

[in，out]标识项目的辅助字符串 (最大 `SCC_PRJPATH_` 大小，包括 null 终止符) 。

 cFiles

中给定的文件数 `lpFilePaths` 。

 lpFilePaths

[in，out]要添加到当前项目中的文件名的数组。

 lpDestination

中要写入文件的目标路径。

 lpComment

中要应用到所添加的每个文件的注释。

 pbResults

[in，out]设置为指示成功 (非零或真) 或失败的标志数组 (零或 FALSE) 对于每个文件， (大小必须至少为 `cFiles` 长的) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_E_PROJNOTOPEN|项目未打开。|
|SCC_E_OPNOTPERFORMED|连接不同于指定的项目 `lpAuxProjPath.`|
|SCC_E_NOTAUTHORIZED|用户无权更新数据库。|
|SCC_E_NONSPECIFICERROR|未知错误。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
