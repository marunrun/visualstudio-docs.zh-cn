---
title: IDebugSymbolProvider::GetAddressesFromContext |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ebd36bdda5059a4fd3c0334a5a2f222aaae40f01
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68206009"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法将文档上下文映射到调试地址的数组。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetAddressesFromContext(   
   IDebugDocumentContext2* pDocContext,  
   BOOL                    fStatmentOnly,  
   IEnumDebugAddresses**   ppEnumBegAddresses,  
   IEnumDebugAddresses**   ppEnumEndAddresses  
);  
```  
  
```csharp  
int GetAddressesFromContext(  
   IDebugDocumentContext2  pDocContext,  
   bool                    fStatmentOnly,  
   out IEnumDebugAddresses ppEnumBegAddresses,  
   out IEnumDebugAddresses ppEnumEndAddresses  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pDocContext`  
 [in]文档上下文中。  
  
 `fStatmentOnly`  
 [in]如果为 TRUE，则限制为单个语句的调试地址。  
  
 `ppEnumBegAddresses`  
 [out]返回与此语句或行关联的起始调试地址的枚举器。  
  
 `ppEnumEndAddresses`  
 [out]返回[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)结束的调试地址与此语句或行关联的枚举器。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 文档上下文通常指示源行组成的范围。 此方法提供的起始和结束调试地址关联使用以下代码行。 某些语言允许跨多个行或包含多个语句的行的语句。 此方法提供了一个标志，用于限制到单个语句的调试地址。  
  
 很可能具有多个调试地址，如下所示的模板大小写的单个语句。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)   
 [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
