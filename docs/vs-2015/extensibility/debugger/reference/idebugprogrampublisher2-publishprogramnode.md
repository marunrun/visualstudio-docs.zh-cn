---
title: IDebugProgramPublisher2：:P ublishProgramNode |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgramNode
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgramNode
ms.assetid: d4b72e04-f726-46cf-8e56-5203ff205b12
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eac08c35afe407358b7e2d37216dda202c490bd3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146300"
---
# <a name="idebugprogrampublisher2publishprogramnode"></a>IDebugProgramPublisher2::PublishProgramNode
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

 (DEs) 和会话调试管理器 (SDM) ，使程序节点可供调试引擎使用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT PublishProgramNode(  
   IDebugProgramNode2 *pProgramNode  
);  
```  
  
```csharp  
int PublishProgramNode(  
   IDebugProgramNode2 pProgramNode  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pProgramNode`  
 中一个 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象，该对象表示要使其可用的程序节点。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法允许在选择和启动程序之前查询信息以进行调试。  
  
 若要从可用性中删除程序节点，请调用 [UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)
