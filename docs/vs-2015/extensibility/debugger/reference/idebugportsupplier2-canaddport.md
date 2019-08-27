---
title: IDebugPortSupplier2::CanAddPort |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e4ec078650446d3511ed9c5bdc8ee3ec0191487d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188352"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

验证端口提供程序可以添加新端口。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT CanAddPort(   
   void   
);  
```  
  
```csharp  
int CanAddPort();  
```  
  
## <a name="return-value"></a>返回值  
 如果可以添加端口，则返回`S_OK`; 否则为返回`S_FALSE`以指示可以将任何端口添加到此端口提供程序。  
  
## <a name="remarks"></a>备注  
 调用此方法之前调用[端口](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)方法因为后一种方法创建该端口，以及添加它，这可能一个耗时的操作。  
  
## <a name="see-also"></a>请参阅  
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
