---
title: IApplicationDebuggerUI 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IApplicationDebuggerUI interface
ms.assetid: b8828817-ca24-4012-802c-7dcaeea65dc8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f138492e5b0a465bb0f101c15457ed1021ab3d5a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991093"
---
# <a name="iapplicationdebuggerui-interface"></a>IApplicationDebuggerUI 接口
由调试器集成的开发环境 (IDE) 实现 (除了`IApplicationDebugger`) 提供更好地控制调试器的用户界面 (UI) 的外部组件。  
  
 除了继承的方法之外`IUnknown`，则`IApplicationDebuggerUI`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IApplicationDebuggerUI::BringDocumentToTop](../../winscript/reference/iapplicationdebuggerui-bringdocumenttotop.md)|用户界面将包含到在调试器中的顶部指定的调试文档的窗口。|  
|[IApplicationDebuggerUI::BringDocumentContextToTop](../../winscript/reference/iapplicationdebuggerui-bringdocumentcontexttotop.md)|引入了包含给定的文档上下文页首调试器用户界面中的窗口和窗口滚动到上下文。|