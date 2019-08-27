---
title: IDebugArrayObject::GetElement |Microsoft Docs
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
ms.sourcegitcommit: da4079f5b6ec884baf3108cbd0519d20cb64c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
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
 [in]元素的索引。  
  
 `ppElement`  
 [out]返回[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口表示的元素。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK;否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法将所有数组对象的元素视为一维数组，即使是多维的数组对象。 例如，给定数组`myarray[3][2][6]`和一个`dwIndex`20 的参数，此方法将返回从元素`myarray[1][1][2]`，和一个`dwIndex`21 参数将返回从元素`myarray[1][1][3]`。 使用[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)方法来确定数组中元素的总数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
