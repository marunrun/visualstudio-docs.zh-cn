---
title: IDebugPortSupplier3::CanPersistPorts |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: edc989771b41cc4a5cc5b4710de4cbb5632873e2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188182"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法确定是否端口提供程序可以保持不变的端口 （通过将它们写入磁盘） 的调试器调用之间。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CanPersistPorts();  
```  
  
```csharp  
int CanPersistPorts();  
```  
  
#### <a name="parameters"></a>参数  
 无。  
  
## <a name="return-value"></a>返回值  
 `S_OK` 如果端口可以保持不变，或`S_FALSE`以指示不能保留端口。  
  
## <a name="remarks"></a>备注  
 如果端口提供程序可以保留端口，它应执行此操作时被销毁并再一次实例化时重新加载它们。  
  
## <a name="see-also"></a>请参阅  
 [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
