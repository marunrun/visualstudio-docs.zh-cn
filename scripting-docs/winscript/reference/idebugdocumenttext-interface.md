---
title: IDebugDocumentText 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentText interface
ms.assetid: 242bad79-9c0a-4a30-879a-9f43db4e022b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8878e1ce6e9ad05fc94b134a2e71847b67d578d2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008610"
---
# <a name="idebugdocumenttext-interface"></a>IDebugDocumentText 接口
提供纯文本版本的调试文档的访问权限。 此接口使用以下约定：  
  
- 字符位置和行号是从零开始。  
  
- 字符位置表示字符偏移量;它们不表示字节或字偏移量。 对于 Win32，字符位置是 Unicode 偏移量。  
  
  除了继承的方法之外`IDebugDocument`，则`IDebugDocumentText`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugDocumentText::GetDocumentAttributes](../../winscript/reference/idebugdocumenttext-getdocumentattributes.md)|返回文档的属性。|  
|[IDebugDocumentText::GetSize](../../winscript/reference/idebugdocumenttext-getsize.md)|返回文档中的行数和字符数。|  
|[IDebugDocumentText::GetPositionOfLine](../../winscript/reference/idebugdocumenttext-getpositionofline.md)|返回字符位置对应的行的第一个字符。|  
|[IDebugDocumentText::GetLineOfPosition](../../winscript/reference/idebugdocumenttext-getlineofposition.md)|返回给定的字符位置的行号和对应的行中的字符偏移量 （可选）。|  
|[IDebugDocumentText::GetText](../../winscript/reference/idebugdocumenttext-gettext.md)|检索字符和/或字符位置范围与关联的字符属性。|  
|[IDebugDocumentText::GetPositionOfContext](../../winscript/reference/idebugdocumenttext-getpositionofcontext.md)|返回与文档上下文相对应的字符位置范围。|  
|[IDebugDocumentText::GetContextOfPosition](../../winscript/reference/idebugdocumenttext-getcontextofposition.md)|创建与提供的字符位置范围对应的文档上下文对象。|