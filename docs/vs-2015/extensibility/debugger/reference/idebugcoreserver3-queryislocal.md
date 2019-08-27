---
title: IDebugCoreServer3::QueryIsLocal | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::QueryIsLocal
helpviewer_keywords:
- IDebugCoreServer3::QueryIsLocal
ms.assetid: cca030de-f853-4ed7-b2fb-395f08a6b884
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 26bed2a60d7412682588a5a39fd6f1301005da01
ms.sourcegitcommit: 0cd282a7584b9bfd4df7882f8fdf3ad8a270e219
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "62569071"
---
# <a name="idebugcoreserver3queryislocal"></a>IDebugCoreServer3::QueryIsLocal
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

确定服务器是否本地给调用方。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT QueryIsLocal(  
   void  
);  
```  
  
```csharp  
int QueryIsLocal();  
```  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`以指示服务器是本地。 返回`S_FALSE`如果服务器运行 msvsmon.exe，通常用于远程调试的实例中。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
