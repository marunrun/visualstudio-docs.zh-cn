---
title: IEnumCodePaths2：： Reset |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumCodePaths2::Reset
helpviewer_keywords:
- IEnumCodePaths2::Reset
ms.assetid: 490c0e19-ff4b-4673-bd06-cdee996ac226
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2f77d1891f51b9e363d5631657a7fde6e442a772
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192027"
---
# <a name="ienumcodepaths2reset"></a>IEnumCodePaths2::Reset
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将枚举重置为第一个元素。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Reset(  
   void  
);  
```  
  
```csharp  
int Reset();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法后， [下一次调用的方法将](../../../extensibility/debugger/reference/ienumcodepaths2-next.md) 返回枚举的第一个元素。  
  
## <a name="see-also"></a>另请参阅  
 [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
