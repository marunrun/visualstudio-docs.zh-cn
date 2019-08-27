---
title: IDebugSymbolProviderDirect |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect interface
ms.assetid: 872b04a8-70de-4ab5-aceb-684c81828545
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1ad768419786f78277b791997538785265a24c0f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153097"
---
# <a name="idebugsymbolproviderdirect"></a>IDebugSymbolProviderDirect
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示元数据和核心符号接口可以直接访问的符号提供程序。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugSymbolProviderDirect: IUnknown  
```  
  
## <a name="methods"></a>方法  
 此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetAppIDFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getappidfromaddress.md)|检索给定的调试地址的应用程序域标识符。|  
|[GetCurrentModulesInfo](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesinfo.md)|检索有关符号组中的模块的信息。|  
|[GetCurrentModulesState](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getcurrentmodulesstate.md)|检索有关符号该组符号提供程序是其成员之一的信息。|  
|[GetMetaDataImport](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmetadataimport.md)|检索元数据导入信息。|  
|[GetMethodFromAddress](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getmethodfromaddress.md)|检索有关指定的调试地址处的方法的信息。|  
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugsymbolproviderdirect-getsymunmanagedreader.md)|检索非托管代码的符号读取器。|  
  
## <a name="remarks"></a>备注  
 此接口可以使用而不是大部分其他符号提供程序接口。 它提供了直接访问元数据和`CorSym`接口。  
  
## <a name="requirements"></a>要求  
 标头：Sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
