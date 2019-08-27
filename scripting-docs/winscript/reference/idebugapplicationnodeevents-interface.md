---
title: IDebugApplicationNodeEvents 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationNodeEvents interface
ms.assetid: 02e0bb17-84ce-458b-bae6-608a9899e535
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7412e258c7f67f44bde6f69b593a1eecb1d84e07
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822270"
---
# <a name="idebugapplicationnodeevents-interface"></a>IDebugApplicationNodeEvents 接口
提供 `IDebugApplicationNode` 接口的事件接口。  
  
 除了继承的方法之外`IUnknown`，则`IDebugApplicationNodeEvents`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugApplicationNodeEvents::onAddChild](../../winscript/reference/idebugapplicationnodeevents-onaddchild.md)|处理事件时的子节点添加到调试应用程序节点对象。|  
|[IDebugApplicationNodeEvents::onRemoveChild](../../winscript/reference/idebugapplicationnodeevents-onremovechild.md)|处理事件时从调试应用程序节点对象中删除的子节点。|  
|[IDebugApplicationNodeEvents::onDetach](../../winscript/reference/idebugapplicationnodeevents-ondetach.md)|处理以表明，分离调试应用程序节点对象从父节点的事件。|  
|[IDebugApplicationNodeEvents::onAttach](../../winscript/reference/idebugapplicationnodeevents-onattach.md)|处理以表明调试应用程序节点对象已附加到父节点的事件。|  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)