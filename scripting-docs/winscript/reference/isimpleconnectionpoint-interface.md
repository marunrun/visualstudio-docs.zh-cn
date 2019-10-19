---
title: ISimpleConnectionPoint 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ISimpleConnectionPoint interface
ms.assetid: f632a82f-942d-4291-963e-e9fa2b162493
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 549d7f38b01937f992b240cb6f1d651bc848236c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571792"
---
# <a name="isimpleconnectionpoint-interface"></a>ISimpleConnectionPoint 接口
提供了一种简单的方法来描述和枚举在特定连接点上激发的事件。 此接口还可以轻松地将 `IDispatch` 对象挂钩到这些事件。 此接口由进程调试管理器（PDM）实现，由脚本引擎使用。  
  
 @No__t_0 提供此接口。  
  
 除了从 `IUnknown` 继承的方法之外，`ISimpleConnectionPoint` 接口还公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[ISimpleConnectionPoint::Advise](../../winscript/reference/isimpleconnectionpoint-advise.md)|在简单连接点对象和客户端接收器之间建立连接。|  
|[ISimpleConnectionPoint::DescribeEvents](../../winscript/reference/isimpleconnectionpoint-describeevents.md)|返回指定事件范围内每个事件的 DISPID 和名称。|  
|[ISimpleConnectionPoint::GetEventCount](../../winscript/reference/isimpleconnectionpoint-geteventcount.md)|返回在此接口上公开的事件数。|  
|[ISimpleConnectionPoint::Unadvise](../../winscript/reference/isimpleconnectionpoint-unadvise.md)|终止先前通过 `ISimpleConnectionPoint::Advise` 建立的通知连接。|  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty 接口](../../winscript/reference/idebugproperty-interface.md)