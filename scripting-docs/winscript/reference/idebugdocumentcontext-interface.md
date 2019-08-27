---
title: IDebugDocumentContext 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentContext interface
ms.assetid: 665ee08a-5c6a-4ab1-ab93-de376acc9a74
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: df4c8b8639a6d4b232f82cf87fff7b069829cc46
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62783189"
---
# <a name="idebugdocumentcontext-interface"></a>IDebugDocumentContext 接口
提供正在调试的一部分文档的抽象表示形式。 文本文档，这种表示形式包含字符位置范围。  
  
 除了继承的方法之外`IUnknown`，则`IDebugDocumentContext`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugDocumentContext::GetDocument](../../winscript/reference/idebugdocumentcontext-getdocument.md)|返回包含此上下文中的文档。|  
|[IDebugDocumentContext::EnumCodeContexts](../../winscript/reference/idebugdocumentcontext-enumcodecontexts.md)|枚举与此文档上下文关联的代码上下文。|