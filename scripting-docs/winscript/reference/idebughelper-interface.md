---
title: IDebugHelper 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugHelper interface
ms.assetid: ef5691e0-1d82-42c2-997c-888e31c478dd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d1708b742a484a2e7d6d48cf759f15c08711e13d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979183"
---
# <a name="idebughelper-interface"></a>IDebugHelper 接口
充当对象浏览器和简单的连接点的工厂。 进程调试管理器 (PDM) 实现此接口，这由脚本引擎。  
  
 除了继承的方法之外`IUnknown`，则`IDebugHelper`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugHelper::CreatePropertyBrowser](../../winscript/reference/idebughelper-createpropertybrowser.md)|返回包装一个变体的属性浏览器。|  
|[IDebugHelper::CreatePropertyBrowserEx](../../winscript/reference/idebughelper-createpropertybrowserex.md)|返回包装变体，并允许自定义转换的变体的值或 VARTYPE 类型为字符串的属性浏览器。|  
|[IDebugHelper::CreateSimpleConnectionPoint](../../winscript/reference/idebughelper-createsimpleconnectionpoint.md)|返回包装的事件接口给定`IDispatch`对象。|