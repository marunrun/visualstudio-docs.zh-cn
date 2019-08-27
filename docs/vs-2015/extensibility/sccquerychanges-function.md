---
title: SccQueryChanges 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: baa6059a1668be5507994921cb96ac3ed1cfd5fe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200014"
---
# <a name="sccquerychanges-function"></a>SccQueryChanges 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数枚举给定的列表的文件，对于每个文件通过回调函数提供有关名称更改的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
SCCRTN SccQueryChanges(  
   LPVOID           pContext,  
   LONG             nFiles,  
   LPCSTR*          lpFileNames,  
   QUERYCHANGESFUNC pfnCallback,  
   LPVOID           pvCallerData  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 pContext  
 [in]源控件插件上下文指针。  
  
 nFiles  
 [in]中的文件数`lpFileNames`数组。  
  
 lpFileNames  
 [in]若要获取其相关信息的文件名称的数组。  
  
 pfnCallback  
 [in]要在列表中每个文件名称调用的回调函数 (请参阅[QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)有关详细信息)。  
  
 pvCallerData  
 [in]值将传递给回调函数保持不变。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|查询过程已成功完成。|  
|SCC_E_PROJNOTOPEN|尚未在源代码管理中打开该项目。|  
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。|  
|SCC_E_NONSPECIFICERROR|未指定或常规时出错。|  
  
## <a name="remarks"></a>备注  
 对其进行查询的更改是对命名空间： 具体而言，重命名、 添加和删除文件。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)   
 [错误代码](../extensibility/error-codes.md)
