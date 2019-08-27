---
title: IDebugAsyncOperation 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugAsyncOperation interface
ms.assetid: ebb2ea75-1443-4d8a-812d-171a166f5f9d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 820ecc40924ace4153b76f46c8b8fd1603512ebb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821778"
---
# <a name="idebugasyncoperation-interface"></a>IDebugAsyncOperation 接口
进程调试管理器实现`IDebugAsyncOperation`接口。 语言引擎将调用`IDebugApplication::CreateAsyncDebugOperation`方法来获取对此接口的引用。 语言引擎可以使用`IDebugAsyncOperation`接口，以提供对同步调试操作的异步访问。  
  
 除了继承的方法之外`IUnknown`，则`IDebugAsyncOperation`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugAsyncOperation::GetSyncDebugOperation](../../winscript/reference/idebugasyncoperation-getsyncdebugoperation.md)|返回与此对象关联的同步调试操作。|  
|[IDebugAsyncOperation::Start](../../winscript/reference/idebugasyncoperation-start.md)|将导致异步操作以开始。|  
|[IDebugAsyncOperation::Abort](../../winscript/reference/idebugasyncoperation-abort.md)|取消操作。|  
|[IDebugAsyncOperation::QueryIsComplete](../../winscript/reference/idebugasyncoperation-queryiscomplete.md)|确定是否已完成调试操作。|  
|[IDebugAsyncOperation::GetResult](../../winscript/reference/idebugasyncoperation-getresult.md)|提供的返回值和返回对象从同步调试操作的参数。|