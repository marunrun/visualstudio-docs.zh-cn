---
title: IDebugTypeFieldBuilder::CreatePrimitive |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- CreatePrimitive
- IDebugTypeFieldBuilder::CreatePrimitive
ms.assetid: 512c6ff0-97c5-409f-939f-4cc969bc4bb9
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5b3119f6fda1b178232c668951b0a5c15004b119
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152926"
---
# <a name="idebugtypefieldbuildercreateprimitive"></a>IDebugTypeFieldBuilder::CreatePrimitive
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

创建表示基元类型的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT CreatePrimitive (  
   DWORD          dwElementType,  
   IDebugField ** pTypeField  
);  
```  
  
```csharp  
int CreatePrimitive (  
   uint            dwElementType,  
   out IDebugField pTypeField  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwElementType`  
 [in]值从[CorElementType 枚举](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)表示基元类型。  
  
 `pTypeField`  
 [out]返回新类型的 IDebugField 接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)
