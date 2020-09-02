---
title: IDebugArrayObject：： GetElement |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElement
helpviewer_keywords:
- IDebugArrayObject::GetElement method
ms.assetid: 08b44341-7bf1-4a8c-8b79-98ae5785b195
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ac59a14a2d3be06c9e1523bcdc0d0ad026e0a7d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423681"
---
# <a name="idebugarrayobjectgetelement"></a>IDebugArrayObject::GetElement
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取数组的元素。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetElement(   
   DWORD          dwIndex,  
   IDebugObject** ppElement  
);  
```  
  
```csharp  
int GetElement(  
   [In] uint dwIndex,   
   out IDebugObject ppElement  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwIndex`  
 中元素索引。  
  
 `ppElement`  
 弄返回表示元素的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法将数组对象的所有元素视为一维数组，即使数组对象是多维的。 例如，假设数组 `myarray[3][2][6]` 和 `dwIndex` 参数为20，则此方法将返回中的元素 `myarray[1][1][2]` ，而 `dwIndex` 参数21会从返回该元素 `myarray[1][1][3]` 。 使用 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) 方法来确定数组中的元素总数。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
