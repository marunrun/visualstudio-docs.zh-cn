---
title: IDebugDocumentHelper 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentHelper interface
ms.assetid: b652a31e-b87b-45f1-b586-94f2b6e822db
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7322ea5e2026ff3f4491ed1106dceb97a5f11c73
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000898"
---
# <a name="idebugdocumenthelper-interface"></a>IDebugDocumentHelper 接口
提供有关进行智能承载所需的多个接口的实现，例如`IDebugDocument`， `IDebugDocumentContext`， `IDebugDocumentProvider`， `IDebugDocumentText`，和`IDebugDocumentTextEvents`接口。  
  
 除了继承的方法之外`IUnknown`，则`IDebugDocumentHelper`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugDocumentHelper::Init](../../winscript/reference/idebugdocumenthelper-init.md)|初始化具有名称和初始属性的调试文档帮助程序。|  
|[IDebugDocumentHelper::Attach](../../winscript/reference/idebugdocumenthelper-attach.md)|将此文档添加到文档树。|  
|[IDebugDocumentHelper::Detach](../../winscript/reference/idebugdocumenthelper-detach.md)|从文档树中删除此文档。|  
|[IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)|将追加结束的 Unicode 字符串的此文档。|  
|[IDebugDocumentHelper::AddDBCSText](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)|将追加一个 DBCS 的字符串来结束本文档。|  
|[IDebugDocumentHelper::SetDebugDocumentHost](../../winscript/reference/idebugdocumenthelper-setdebugdocumenthost.md)|集`IDebugDocumentHost`此文档。|  
|[IDebugDocumentHelper::AddDeferredText](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)|给定的文本可用，但它不提供字符通知帮助器。|  
|[IDebugDocumentHelper::DefineScriptBlock](../../winscript/reference/idebugdocumenthelper-definescriptblock.md)|表示特定范围的字符是一个由给定的脚本引擎处理的脚本块帮助程序。|  
|[IDebugDocumentHelper::SetDefaultTextAttr](../../winscript/reference/idebugdocumenthelper-setdefaulttextattr.md)|设置要用于不是将脚本块中的文本的默认特性。|  
|[IDebugDocumentHelper::SetTextAttributes](../../winscript/reference/idebugdocumenthelper-settextattributes.md)|在范围内的文本上设置的特性。|  
|[IDebugDocumentHelper::SetLongName](../../winscript/reference/idebugdocumenthelper-setlongname.md)|设置文档的长名称。|  
|[IDebugDocumentHelper::SetShortName](../../winscript/reference/idebugdocumenthelper-setshortname.md)|设置文档的短名称。|  
|[IDebugDocumentHelper::SetDocumentAttr](../../winscript/reference/idebugdocumenthelper-setdocumentattr.md)|设置本文档的特性。|  
|[IDebugDocumentHelper::GetDebugApplicationNode](../../winscript/reference/idebugdocumenthelper-getdebugapplicationnode.md)|返回对应于本文档的调试应用程序节点。|  
|[IDebugDocumentHelper::GetScriptBlockInfo](../../winscript/reference/idebugdocumenthelper-getscriptblockinfo.md)|检索一的系列字符和对应的脚本块的脚本引擎。|  
|[IDebugDocumentHelper::CreateDebugDocumentContext](../../winscript/reference/idebugdocumenthelper-createdebugdocumentcontext.md)|创建新的调试文档上下文。|  
|[IDebugDocumentHelper::BringDocumentToTop](../../winscript/reference/idebugdocumenthelper-bringdocumenttotop.md)|本文档提供在调试器中的顶部对用户界面。|  
|[IDebugDocumentHelper::BringDocumentContextToTop](../../winscript/reference/idebugdocumenthelper-bringdocumentcontexttotop.md)|调试器用户界面中赋予顶部本文档的上下文。|