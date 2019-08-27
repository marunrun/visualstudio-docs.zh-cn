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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147950"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数确定源代码管理插件是否支持 MSSCCPRJ 创建。每个给定文件的源代码管理文件。  
  
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
 [in]源控件插件上下文指针。  
  
 nFiles  
 [in]文件名称中包含的数量`lpFileNames`数组的长度以及`pbSccFiles`数组。  
  
 lpFileNames  
 [in]若要检查的完全限定的文件名称的数组 （数组必须由调用方已分配）。  
  
 pbSccFiles  
 [in、 out]要在其中存储结果的数组。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|成功。|  
|SCC_E_INVALIDFILEPATH|一个数组中的路径是无效的。|  
|SCC_E_NONSPECIFICERROR|非特定故障。|  
  
## <a name="remarks"></a>备注  
 使用一组文件，以确定是否 MSSCCPRJ 中支持的源代码管理插件调用此函数。SCC 文件为每个给定文件 （针对 MSSCCPRJ 的详细信息。SCC 文件，请参阅[MSSCCPRJ。SCC 文件](../extensibility/mssccprj-scc-file.md))。 源代码管理插件可以声明其是否具有创建 MSSCCPRJ 的功能。SCC 文件通过声明`SCC_CAP_SCCFILE`在初始化过程中。 该插件返回`TRUE`或`FALSE`为每个文件`pbSccFiles`数组指示哪些给定文件具有 MSSCCPRJ。SCC 的支持。 如果该插件从函数返回成功代码，将遵循返回数组中的值。 在失败时，该数组将被忽略。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)
