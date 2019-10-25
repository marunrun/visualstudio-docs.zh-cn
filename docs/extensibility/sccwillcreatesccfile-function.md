---
title: SccWillCreateSccFile 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2ac7657258b79b2e53bee8138bc5b2728f618eac
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720121"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 函数
此函数确定源代码管理插件是否支持创建 MSSCCPRJ.SCC。每个给定文件的 SCC 文件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccWillCreateSccFile(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPBOOL  pbSccFiles
);
```

#### <a name="parameters"></a>参数
 pContext

中源代码管理插件上下文指针。

 n

中@No__t_0 数组中包含的文件名以及 `pbSccFiles` 数组的长度。

 lpFileNames

中要检查的完全限定文件名称的数组（必须由调用方分配数组）。

 pbSccFiles

[in，out]要在其中存储结果的数组。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_INVALIDFILEPATH|数组中的某个路径无效。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数使用文件列表进行调用，以确定源代码管理插件是否在 MSSCCPRJ.SCC 中提供支持。每个给定文件的 SCC 文件（有关 MSSCCPRJ.SCC 的详细信息。SCC 文件，请参阅[mssccprj.scc。SCC 文件](../extensibility/mssccprj-scc-file.md)）。 源代码管理插件可以声明它们是否具有创建 MSSCCPRJ.SCC 的功能。SCC 文件，方法是在初始化过程中声明 `SCC_CAP_SCCFILE`。 此插件返回 `pbSccFiles` 数组中每个文件 `TRUE` 或 `FALSE`，以指示给定的文件中 MSSCCPRJ.SCC。SCC 支持。 如果插件从函数返回成功代码，则返回数组中的值。 失败时，将忽略数组。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)