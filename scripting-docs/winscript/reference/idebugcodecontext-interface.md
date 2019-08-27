---
title: IDebugCodeContext 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext interface
ms.assetid: ae1264d5-1ac2-4b04-9fa5-958212543975
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f3d3d1834d176a323778ae9b7d215951d1a26bb4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821739"
---
# <a name="idebugcodecontext-interface"></a>IDebugCodeContext 接口
表示可执行代码中的位置的抽象。  
  
 除了继承的方法之外`IUnknown`，则`IDebugCodeContext`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugCodeContext::GetDocumentContext](../../winscript/reference/idebugcodecontext-getdocumentcontext.md)|返回与此代码的上下文关联的文档上下文。|  
|[IDebugCodeContext::SetBreakPoint](../../winscript/reference/idebugcodecontext-setbreakpoint.md)|设置或清除断点在此代码的上下文。|