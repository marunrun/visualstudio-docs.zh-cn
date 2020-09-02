---
title: SccWillCreateSccFile 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb0df475098a0fb0675327cece6dd9c643a0c4d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68147950"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数确定源代码管理插件是否支持创建 MSSCCPRJ.SCC。每个给定文件的 SCC 文件。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
 中数组中包含的文件名以及 `lpFileNames` 数组的长度 `pbSccFiles` 。  
  
 lpFileNames  
 中要检查 (数组的完全限定文件名的数组必须由调用方) 分配。  
  
 pbSccFiles  
 [in，out]要在其中存储结果的数组。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|成功。|  
|SCC_E_INVALIDFILEPATH|数组中的某个路径无效。|  
|SCC_E_NONSPECIFICERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 此函数使用文件列表进行调用，以确定源代码管理插件是否在 MSSCCPRJ.SCC 中提供支持。每个给定文件的 SCC 文件 (获取有关 MSSCCPRJ.SCC 的详细信息。SCC 文件，请参阅 [mssccprj.scc。SCC 文件](../extensibility/mssccprj-scc-file.md)) 。 源代码管理插件可以声明它们是否具有创建 MSSCCPRJ.SCC 的功能。SCC 文件 `SCC_CAP_SCCFILE` 在初始化期间声明。 该插件返回 `TRUE` `FALSE` 数组中的或每个文件 `pbSccFiles` ，以指示给定文件中的哪些 mssccprj.scc。SCC 支持。 如果插件从函数返回成功代码，则返回数组中的值。 失败时，将忽略数组。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)
