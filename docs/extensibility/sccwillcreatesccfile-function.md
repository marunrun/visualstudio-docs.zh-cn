---
title: Sccwill 创建sccfile功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0694fd6b4ba82faf8b05354765fc5734efe2ef4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700202"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 函数
此功能确定源代码管理插件是否支持 MSSCCPRJ 的创建。每个给定文件的 SCC 文件。

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

[在]源代码管理插件上下文指针。

 n文件

[在]`lpFileNames`数组中包含的文件名数以及`pbSccFiles`数组的长度。

 lpFile名称

[在]要检查的完全限定文件名数组（数组必须由调用方分配）。

 pbScc文件

[进出]用于存储结果的数组。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_INVALIDFILEPATH|数组中的一个路径无效。|
|SCC_E_NONSPECIFICERROR|非特异性故障。|

## <a name="remarks"></a>备注
 使用文件列表调用此功能，以确定源代码管理插件是否在 MSSCCPRJ 中提供支持。每个给定文件的 SCC 文件（有关 MSSCCPRJ 的详细信息。SCC 文件，请参阅[MSSCCPRJ。SCC 文件](../extensibility/mssccprj-scc-file.md)。 源代码管理插件可以声明它们是否具有创建 MSSCCPRJ 的功能。通过在初始化期间声明`SCC_CAP_SCCFILE`SCC 文件。 插件返回`TRUE`或`FALSE`数组中的`pbSccFiles`每个文件，以指示哪些给定文件具有 MSSCCPRJ。SCC 支持。 如果插件返回函数中的成功代码，则将尊重返回数组中的值。 发生故障时，将忽略数组。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)
